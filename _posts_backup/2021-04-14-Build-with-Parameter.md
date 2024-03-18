---
title: "[Jenkins] Build with Parameter"
categories: [Jenkins]
tags: [Jenkins]
comments: true 
img_path: /assets/images/Jenkins/
---

고객사에서 프로그램을 외부에서 사용해야 하는데 프로그램 유출이 우려되어 보안 기능을 적용해달라고 합니다.

고객사에서 제시한 기능은 다음과 같습니다.

1. 프로세스 체크(특정 프로세스가 돌아가고 있는지 확인)
2. 라이선스 키 체크
3. 만료 기간 설정


첫 번째는 요새 기업에서는 보안 프로그램이 돌아가고 있기 때문에 그걸 체크해달라는 겁니다.

두, 세 번째는 JWT를 사용하여 기능을 구현하였습니다.

​

이제 Jenkins를 이용하여 보안 기능이 적용된 설치 파일을 만들어야 합니다.

참고로 보안 기능을 위해  git에 새로운 브랜치를 만들었습니다. 따라서 빌드할 때 브랜치를 선택해야 합니다.

Jenkins의 Build with Parameter 플러그인을 이용하면 빌드할 때 브랜치를 선택할  수 있습니다.

​

다음과 같이 Job에 매개변수를 추가합니다.

![](2021-04-14-1.png)


브랜치 이름을 선택할 수 있도록 선택 파라미터로 2개의 브랜치 이름을 추가하였습니다.
​

[소스 코드 관리] 항목에 사용자가 선택한 브랜치 이름을 적용합니다.

![](2021-04-14-2.png)

이제 빌드 후 메일 통보에 선택한 브랜치에 따라 설치 파일 이름을 다르게 나타나도록 합니다.

Email Extension에 설치 파일 이름을 넘기기 위해 Environment variables through a file 플러그인을 사용하였습니다.

![](2021-04-14-3.png)


PowerShell을 이용하여 propfile에 환경 변수를 쓰면 됩니다. BUILD_NAME, OUTPUT_FILE_NAME 두 개를 저장하였습니다.

환경 변수를 서로 다른 줄에 저장하기 위해 `r`n을 넣어 줄 바꿈을 하였습니다.

```sh
Out-File -FilePath .\propfile -InputObject "BUILD_NAME=$version`r`nOUTPUT_FILE_NAME=$env:BRANCH" -Encoding ASCII
```

Email Extension template 파일에서 build.getEnvVars()를 이용하여 환경 변수에 접근할 수 있습니다.


빌드가 끝나면 아래와 같은 메일이 발송됩니다.

![](2021-04-14-4.png)

설정이 끝나면 Job에 Build with Parameters 항목이 생깁니다. 브랜치를 선택하여 빌드를 할 수 있습니다.

![](2021-04-14-5.png)