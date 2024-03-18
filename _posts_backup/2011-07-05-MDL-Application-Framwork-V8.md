---
title: "MDL Application Framwork XM"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM]
---

인도에서 일을 하는데 시간이 잘 안가네요.
아무리 자기 집이 보잘것 없더라도 집만한 곳이 없다는 말이 맞는것 같아요.\
![](2011-07-05-13.jpg)\


MSTN XM 부터는 MS Studio의 기능을 사용하여 프로그램을 작성할수 있습니다.\
GUI도 MFC를 사용하여 작성할 수 있구요.(J에서 GUI를 작성하는 어려움에 비하면 엄청나게 발전한 것입니다.)

앞으로 MSTN XM에서의 몇가지 Sample Code를 올릴 예정입니다.

우선 resource 파일을 살펴보도록 합시다.
```c
#include rscdefs.h>

#define DLLAPPID 1

/* associate app with dll */
/* MicroStation has it's own compiler and */
/*also has it's own development language*/
/*to create relationship between .ma and .dll*/
/*we need to do following step. which is entry point*/

 DllMdlApp DLLAPPID =
{
    //   MDL Application name     VC++DLL in MDLAPPS or %PATH%
    "BasicApp_Suther","BasicApp_Suther.dll"
}
```

이 부분(30 ~ 34째 줄)이 J의 resource 파일 부분과 다른 부분인데요,
설명에서 알수 있듯이 .ma 파일과 연관된 .dll 파일을 정의하는 부분입니다.

이 부분을 통해서 코드의 대부분을 .ma 파일에 아닌 .dll 파일에 넣을수 있습니다.