---
title: "XM MDL Programming - #1"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

XM MDL 프로그래밍을 하면 크게 *.ma 파일과 *.dll 파일이 생깁니다.\
*.ma 파일에는 거의 아무런 정보를 가지고 있지 않고 dll의 링크 정보를 가지고 있습니다.\
대부분의 소스 코드는 컴파일 되어 dll 파일로 생기게 됩니다.\

ma 파일은 전통적으로 MSTN 컴파일러로 만듭니다.(make 파일등이 필요합니다.)

dll 파일은 MS Visual Studio 컴파일러가 만듭니다. 따라서 MS Visual Studio의 여러가지 기능들을 MDL Application에서 사용할수 있습니다.(MFC , STL , etc)\
MSTN XM용 MDL 프로그램을 만들기 위해서는 MS Visual Studio 2003을 사용하여야 합니다.

자 그럼 코드 조각을 살펴볼까요? 참, .ma 파일을 만드는 쪽에서는 main함수를 포함하지 않아야 합니다.

참 먼저 MFC DLL로 프로젝트를 하나 만들어야 합니다.

```cpp
/*******************************************************************************************//* -INFORMATION
As you probably know, C++ mangles function names. This is how it lets you implement
function overloading,when a function has multiple signatures and multiple implementations.
Unfortunately,C++ mangles function names whether it needs to or not.
For example, even when there is only one version of a function,
C++ mangles its name. Unless you do something,
C++ will change MdlMain to something that MicroStation can't understand,
such as MdlMainAPQC01ABR56TuV.

A way to prevent name mangling is to wrap your C functions in scope extern "C" {}.
This tells the compiler to use C rather than C++ to compile code within that scope.
Defeat the C++ compiler like this ?
********************************************************************************************/

/*******************************************************************************************/
//Function:extern "C" DLLEXPORT  int MdlMain
//Desc:Entry point of the program.
//******************************************************************************************/
extern "C" DLLEXPORT  int MdlMain
(
    int         argc,
    char        *argv[]
)
{
    AFX_MANAGE_STATE(AfxGetStaticModuleState());

    mdlOutput_message("Hello MDL World!!!");

    return SUCCESS;
}
```

MDL Application을 위한 Entry 포인터로 MdlMain 함수를 작성해야 합니다.\
위의 코드를 보시면 아시겠지만 "Hello MDL World"를 상태바에 출력하는 예제입니다.\
물론 MDL 관련 헤더 파일과 라이브러리를 링크시켜야만 합니다.\
이에 관련해서는 파일을 첨부합니다.\
컴파일을 하면 dll 파일이 생성됩니다.

그리고 MSTN 컴파일러를 가지고 ma 파일을 생성해야 합니다.\
ma 파일을 생성하는 방법은 아래 MSTN J 관련 MDL 프로그래밍 부분을 살펴보세요.\
첨부한 파일에서는 proj 폴더의 build_XM.cmd 파일을 실행시키면 ma 파일을 생성합니다.

만일 .ma 파일이 main 함수를 가지고 있다면 main함수가 호출되고  MdlMain함수는 호출되지 않습니다.
![](2011-07-05-14.jpg)