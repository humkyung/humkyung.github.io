---
title: "XM MDL Programming - #8(Visual Studio Project 생성하기)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

순서가 뒤바뀐 감이 없지 않지만, 이번에는 Visual Stuido Project를 생성하여 설정을 하는 방법에 대해서 알아보도록 합시다.

일단은 MFC DLL 프로젝트를 하나 생성합니다. 기본값으로 그냥 생성하시면 됩니다.

그리고 SDK가 설치되어 있는 폴더를 설정합니다.
![](2011-07-05-33.jpg)


다음에는 Preprocessor를 설정합니다.\
아래 그림과 같이 winNT를 추가합니다. 그리고 디버깅 모드일때는 _DEBUG를 _DEBUG_BUILD로 변경해주세요.
![](2011-07-05-34.png)


디버깅 모드일 때 코드 생성의 런타임 라이브러리를 아래와 같이 (/MDd)로 변경해주세요.
![](2011-07-05-35.png)

 
Compiled Header를 <code style="color:red">Create Precompiled Header (/Yc)<code>로 설정해 주세요.
 
Linker에서 Additional Library Directory를 설정합니다.
![](2011-07-05-36.jpg)
 
 
그리고 추가 Library를 등록합니다. 기본적인 Library항목은 아래와 같습니다.\
<code style="color:red">toolsubs.lib dgnfileio.lib ditemlib.lib mdlbltin.lib nativewindow.lib nativewinmfc.lib mdllib.lib</code>


UI를 만들지 않는다면 <code style="color:red">nativewindow.lib nativewinmfc.lib</code> 이를 링크해 줄 필요가 없습니다.\
이렇게 하면 기본적인 프로젝트 설정이 끝납니다.~~