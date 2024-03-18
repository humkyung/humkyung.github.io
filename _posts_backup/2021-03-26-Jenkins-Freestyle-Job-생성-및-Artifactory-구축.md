---
title: "Jenkins Freestyle Job 생성 및 Artifactory 구축"
categories: [Jenkins, Artifactory]
tags: [Jenkins, Freestyle, Artifactory, 젠킨스, 아티팩토리]
comments: true 
img_path: /assets/images/Jenkins/
---

Jenkins Freestyle Job에 대해 알아보도록 하겠습니다.

## Jenkins 설정

1.1 사용자 정보(Credential)은 Manage Credential 화면에서 추가할 수 있습니다.

![](2021-03-26-1.png)

1.2 Plugin 설치

 - MSBuild Plugin: MSBuild를 사용하기 위해서는 MSBuild Plugin을 설치하셔야 합니다.\
 ![](2021-03-26-2.png)


- change-assembly-version-plugin : .NET 프로젝트의 어셈블리 정보를 수정할때 필요합니다.\
![](2021-03-26-3.png)

- Environment File Plugin : 파일의 정보로 환경 변수를 바꿀때 사용합니다.\
![](2021-03-26-4.png)

- Email Extension Plugin : html 형식의 메일을 발송할때 사용합니다.\
![](2021-03-26-5.png)


1.3 Jenkins 환경 설정

- Global properties를 설정합니다. 프로젝트 빌드에 필요한 파일들의 경로를 설정하였습니다.\
![](2021-03-26-6.png)


- 빌드 결과를 통보하기 위해 Email 설정을 합니다.\
![](2021-03-26-7.png)


- .NET 프로젝트를 MSBuild로 컴파일하기 때문에 필요한 Global Tool Configuration에서 MSBuild 를 추가합니다.\
![](2021-03-26-8.png)


2. Job 생성 및 설정

2.1 우선 Freestyle Project로 Job을 생성합니다.\
![](2021-03-26-9.png)


2.2 [Job 구성] 소스를 받기위해 소스 저장소 정보를 입력합니다.

저희 회사는 Git을 사용하고 있습니다. 그리고 소스 저장소에 접근하기 위해 사용자 정보를 설정합니다.\
![](2021-03-26-10.png)


2.3 빌드 환경을 설정합니다. 빌드할때마다 Workspace를 삭제하고 환경 변수를 설정할 파일 경로를 입력합니다.

환경 변수 파일에 BUILD_NAME를 저장하면 환경 변수가 변경이 되고 이후에 설명할 Email template 파일에서 BUILD_NAME을 읽어서 메일에 버전을 표시하게 됩니다. 따라서 BUILD_NAME은 Global properties에 등록이 되어 있어야 합니다.\
![](2021-03-26-11.png)


2.4 빌드

- 어셈블리의 빌드 번호를 Jenkins의 BUILD_NUMBER로 변경합니다. 컴파일된 실행 파일의 빌드 번호가 Jenkins의 BUILD_NUMBER로 설정됩니다.\
![](2021-03-26-12.png)

- NUGET을 이용하여 프로젝트에 필요한 패키지들을 설치합니다. 여기서 NUGET은 Global properties에 설정되어야 합니다.\
![](2021-03-26-13.png)


- MSBuild를 이용하여 프로젝트를 빌드합니다.\
![](2021-03-26-14.png)


- 빌드 파일들을 설치 파일로 만듭니다. 실행 파일에서 버전 정보를 읽어와 설치 파일 스크립트(*.wxs)에 반영합니다.

이렇게 하면 실행 파일과 설치 파일의 버전이 같게됩니다.\
![](2021-03-26-15.png)


- 생성한 설치 파일을 Artifactory에 배포합니다.\
![](2021-03-26-16.png)


- 빌드 결과를 메일로 발송합니다.\
![](2021-03-26-17.png)


[Advanced Setting]에서 [Add Triger]를 이용하여 빌드 결과에 따라 메일 발송 여부를 결정할 수 있습니다.\
![](2021-03-26-18.png)\
![](2021-03-26-19.png)
_빌드 결과 메일_

환경 변수 파일로 갱신한 환경 변수 BUILD_NAME이 파일 이름으로 들어가 있는걸 알수 있습니다.

---

## Artifactory 설치

1. https://jfrog.com/open-source/에서 최신 Artifactory 를 다운받습니다. open-source 버전도 설치 파일을 배포하는데는 무리가 없습니다.\
저희들은 윈도우용을 다운받았습니다.

2. 압축 해제합니다.

3. installService.bat 파일을 관리자 권한으로 실행합니다. Artifactory라는 이름으로 서비스가 등록됩니다.\
![](2021-03-26-20.png)

4. Artifactory의 로그온 속성에서 "서비스와 데스크톱 상호 작용 허용(W)"을 체크합니다.\
![](2021-03-26-21.png)

5. 방화벽에서 8081-8082를 해제합니다.\
![](2021-03-26-22.png)

6. http://localhost:8081에 접속합니다. Artifactory의 기본 포트가 8081입니다.\
![](2021-03-26-23.png)

7. admin/password로 로그인하여 관리자의 속성을 변경합니다.\
![](2021-03-26-24.png)

8. General Settings에서 Custom Base URL을 설정합니다.\
![](2021-03-26-25.png)

9. Repositories에서 Generic Type으로 Local Repository를 추가합니다.\
![](2021-03-26-26.png)