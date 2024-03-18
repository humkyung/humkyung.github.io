---
title: "[Jenkins] Pipeline Job 구축"
categories: [Jenkins]
tags: [Jenkins, Pipeline]
comments: true 
img_path: /assets/images/Jenkins/
---

Pipeline 프로젝트를 생성하기 위해서는 Groovy 스크립트를 알아야 합니다.

하지만 Freestyle 프로젝트보다는 스크립트를 사용하기 때문에 한 군데서 빌드 흐름을 제어가 가능합니다.

Freestyle의 경우는 설정하는 부분이 여기저기 흩어져 있어 설정하기에 산만한 것 같습니다.

<a href="https://blog.naver.com/PostView.nhn?blogId=rudnfskf2&logNo=221470021793&categoryNo=58&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=search&userTopListOpen=true&userTopListCount=5&userTopListManageOpen=false&userTopListCurrentPage=1">여기</a>을 참조하면 좋을것 같습니다.​


아래 2가지 종류의 프로젝트에 대해서 Jenkins 파이프 라인을 구축하였습니다. 둘다 흐름은 동일합니다.

***.NET 프로젝트 파이프라인***\
![](2021-03-20-1.png)

***파이썬 프로젝트의 파이프라인***\
![](2021-03-20-2.png)

우선 Jenkins의 ***"시스템 설정"*** 에서 프로젝트 빌드에 필요한 환경 변수들을 설정합니다.

 - 버전별 Python 실행 파일 경로 : Python 프로젝트 컴파일에 필요합니다.
 - MsBuild.exe 파일 경로 : .NET 솔류션 컴파일에 필요합니다.
 - WixToolSet 파일 경로들 : 설치 파일 생성에 필요합니다.
 - CURL, DOXYGEN .... : 필요한 파일들을 추가합니다.
![](2021-03-20-3.png)

## git에서 소스 얻어오기
> git에 접속하여 소스를 얻어올 사용자의 Credential을 추가합니다. ID/PASSWORD를 입력하면 됩니다.\
![](2021-03-20-4.png)\
```groovy
stage('Checkout') {
    steps {
        git branch: 'master', credentialsId: 'Your credentials id', url: '{Repository Path}'
    }
}
```

## Python 가상 환경 구축
> <a href="https://blog.naver.com/zbaekhk/222280002524">여기</a> 참조하시면 됩니다.

## 버전 수정
> Jenkins로 빌드할 때마다 Jenkins BUILD_NUMBER로 실행 파일 및 설치 파일의 빌드 넘버를 설정하도록 합니다.<br>
> MSDN을 찾아보면 빌드 넘버는 Major.Minor.Build.Revision으로 구성되어 있습니다.<br>
> Python 프로젝트의 경우 세번째 Build를 PowerShell을 사용하여 Jenkins의 BUILD_NUMBER로 설정해줍니다.
> .NET의 AssemblyInfo.cs의 버전 정보는 powershell로는 변경이 어려워 C#으로 초간단한 프로그램을 작성하였습니다.\
> 인자로 AssemblyInfo.cs 파일 경로와 BUILD_NUMBER를 받습니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using System.Text.RegularExpressions;

namespace ConsoleApp1
{
    class Program
    {
        static void Main(string[] args)
        {
            if(args.Length == 2 && File.Exists(args[0]))
            {
                List<string> oNewList = new List<string>();

                string[] lines = System.IO.File.ReadAllLines(args[0]);
                foreach (string line in lines)
                {
                    if(line.StartsWith("[assembly: AssemblyVersion(\""))
                    {
                        int length = "[assembly: AssemblyVersion(\"".Length;
                        string version = line.Substring(length, line.Length - length - 3);
                        string[] tokens = version.Split('.');
                        oNewList.Add($"[assembly: AssemblyVersion(\"{tokens[0]}.{tokens[1]}.{args[1]}.{tokens[3]}\")]");
                    }
                    else if(line.StartsWith("[assembly: AssemblyFileVersion(\""))
                    {
                        int length = "[assembly: AssemblyFileVersion(\"".Length;
                        string version = line.Substring(length, line.Length - length - 3);
                        string[] tokens = version.Split('.');
                        oNewList.Add($"[assembly: AssemblyFileVersion(\"{tokens[0]}.{tokens[1]}.{args[1]}.{tokens[3]}\")]");
                    }
                    else
                    {
                        oNewList.Add(line);
                    }
                }

                File.WriteAllLines(args[0], oNewList);
            }
        }
    }
}
```

```bat
bat "${ChangeAssembly} ${WORKSPACE}/DTI_PID/PDF_TO_IMAGE/Properties/AssemblyInfo.cs ${env:BUILD_NUMBER}"
```

위 코드에서 만들어 시스템 설정에 추가한 ChangeAssembly는 ${ChangeAssembly} 형식으로 호출합니다.\
<i>//  PYTHON</i>\
<i>// version.rc 파일을 열어 {BUILD_NUMBER} 텍스트를 Jenkins의 BUILD_NUMBER 값으로 바꾸어 저장합니다.</i>

```powershell
powershell """(get-content ${WORKSPACE}/version.rc) | % {\$_ -replace '{BUILD_NUMBER}',${env:BUILD_NUMBER}} | Out-File ${WORKSPACE}/version.rc -Encoding ASCII"""
```

## 패키지 업데이트
    3.1 Python 패키지 업데이트
    > 이전 글을 참조하시면 패키지 목록을 추출하여 텍스트 파일을 만드는 방법과 반대로 목록 파일을 이용하여 패키지를 설치하는 방법을 확인할 수 있습니다.\
    > pip install -r requirements.txt

    3.2 Nuget 패키지 업데이트
    > nuget.exe와 packages.config 파일을 이용하여 Nuget 패키지를 업데이트합니다.\
    nuget.exe에 대한 자세한 내용은 <a href="https://learn.microsoft.com/ko-kr/nuget/reference/cli-reference/cli-ref-restore">여기</a> 서 확인할 수 있습니다.\
    nuget restore a.sln -PackageDirectory ..\packages

## 컴파일

    4.1 PyInstaller를 이용하여 Python 프로젝트 컴파일
    > App.spec 파일은 컴파일하기 위한 설정 파일입니다.\
    PyInstaller App.spec --onedir -p PyQt5 -w --log-level=DEBUG --hidden-import=tkinter,pyqtgraph,getmac -y

    4.2 MsBuild.exe를 이용하여 .NET 프로젝트 컴파일
    > 솔류션 혹은 프로젝트 파일을 빌드 모드, 출력 경로를 설정하여 컴파일합니다.\
    ${MSBUILD_VS2017} a.sln -p:Configuration=Release;OutputDirectory=..\Setup\
    MSBUILD_VS2017로 시스템 설정에 MSBUILD.exe 경로를 등록했습니다.

## 설치 파일 생성

     WixToolSet을 이용하여 설치 파일을 생성합니다. 흐름은 아래와 같습니다.\
    ![](2021-03-20-5.png)

```sh
$version=(get-item ./dist/App/XXXX.exe).VersionInfo.FileVersion
(get-content ./XXXX.wxs) | % {$_ -replace '{VERSION}',$version} | Out-File ./XXXX.wxs -Encoding ASCII
${CANDLE} ".\A.wxs" -out .\Setup\
${LIGHT} -out ".\Setup\A-%1.msi" ".\Setup\A.wixobj" -ext WixUIExtension -ext WixUtilExtension
```
## 아티팩토리에 배포
> CURL 실행 파일을 이용하여 생성한 설치 파일을 Artifactory에 등록합니다. 저희는 JFrog의 Artifactory-OSS를 사용하고 있습니다.

```sh
${CURL} -uID:Password -X PUT "http://host/artifactory/AViewer/A-%1.msi" -T "./Setup/A-%1.msi"
```

## 빌드 결과 메일 발송
> 빌드 결과 메일을 프로젝트 관련자들에게 발송합니다.\
html template 파일을 사용하면 훌륭한 빌드 결과물을 받아 볼 수 있습니다.\
html template 파일을 작성하여 Jenkins의 email-templates 폴더에 저장해 둬야 합니다.
![](2021-03-20-6.png)\
html template 까지 등록했는데 html이 표시되지 않고 에러가 발생할 때가 있습니다.\
![](2021-03-20-7.png)
Jenkins 관리에 가서 스크립트가 실행 가능하도록 승인해줘야 합니다.\
![](2021-03-20-8.png)
이제 제대로 된 결과 메일을 받을 수 있습니다. 하지만 빌드 실패 메일이네요....\
![](2021-03-20-9.png)