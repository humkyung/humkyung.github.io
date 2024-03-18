---
title: "SonarQube와 Jenkins 연동"
categories: [Jenkins, SonarQube]
tags: [Jenkins, SonarQube]
comments: true 
img_path: /assets/images/Jenkins/
---

Jenkins와 연동하기 위해서 SonarQube Scanner for Jenkins 플러그인을 설치합니다.\
![](2021-04-08-1.png)

SonarQube에서 프로젝트를 생성합니다.\
![](2021-04-08-2.png)

Project key로 프로젝트 이름을 입력합니다. 그리고 Set Up 버튼을 클릭합니다.\
![](2021-04-08-3.png)


토큰을 생성하기 위해 프로젝트 이름을 입력하고 [생성하기] 버튼을 클릭합니다.\
![](2021-04-08-4.png)


생성한 토큰은 저장합니다. 이 페이지를 벗어나면 생성한 토큰을 찾을 방법이 없습니다.

[Continue] 버튼을 클릭합니다.\
![](2021-04-08-5.png)


프로젝트에서 사용하는 주요 언어를 선택합니다.

기타를 선택했을 경우 운영체제까지 선택해줍니다.\
![](2021-04-08-6.png)


SonarQube Scanner를 다운로드합니다. 다운로드한 파일을 Jenkins가 구축되어 있는 시스템에 설치합니다.\
![](2021-04-08-7.png)


Sonar Scanner 실행 예제를 Jenkins Job에 복사, 붙여넣기 합니다. 그러면 Jenkins에서 프로젝트를 빌드할때 마다 SonarQube에서 소스를 검사하게 됩니다.

Python 프로젝트를 SonarQube 를 통해 소스 검사를 했는데 에러가 발생했습니다.\
![](2021-04-08-8.png)


분명 Python 프로젝트인데 왜 node 를 찾는지 모르겠네요. 이런 현상을 구글링해보니 프로젝트 속성에 node 경로를 넣어주면 된다고 합니다.\
![](2021-04-08-9.png)

sonar-project.properties 파일을 만들어 프로젝트 최상위 폴더에 추가하였습니다. 에러없이 잘 돌아갑니다.\
![](2021-04-08-10.png)

검사 결과는 SonarQube 대시보드에서 확인할 수 있습니다. 회사 사람들 모두가 볼수 있도록 입구 TV 같은 곳에 켜놓으면 프로젝트 상황을 볼수 있어 더욱 효과적일것 같습니다.\
![](2021-04-08-11.png)