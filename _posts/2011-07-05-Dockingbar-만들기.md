---
title: "Dockingbar 만들기"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM, Dockingbar]
---

Arx에서도 MDL에서도 Dockingbar는 인기가 많은 모양입니다.\
V8i에서 사용가능한 Dockingbar를 만들어 달라고 해서 한번 만들어 봤습니다.


여기서 가장 핵심은 Microstation SDK의 CBNETDockableDialog 클래스를 사용한다는 겁니다.
이 클래스를 사용하면 손쉽게 도킹바를 만들수 있습니다.


우선 결과부터 먼저 보시죠(실제 코딩은 거의 없기 때문에...)\
![](2011-07-05-61.png)\
![](2011-07-05-62.png)

       
전체적인 흐름은 앞서 설명한 것과 동일하고요,


도킹바로 사용할 다이얼로그를 하나 만들고 거기서 클래스 하나를 생성합니다.
```cpp
#pragma once

#include <mfc/CBNETDockableDialog.h>

// CDockableDialog dialog

class CDockableDialog : public CBNETDockableDialog
{
    DECLARE_DYNAMIC(CDockableDialog)

public:
    CDockableDialog(TCHAR *pTitle = NULL);   // standard constructor
    virtual ~CDockableDialog();

// Dialog Data
    enum { IDD = IDD_DOCKABLE };

protected:
    virtual void DoDataExchange(CDataExchange* pDX);    // DDX/DDV support

    DECLARE_MESSAGE_MAP()
};
```

그리고 MdlMain 함수에서 도킹바를 생성합니다.
```cpp
/*******************************************************************************************/
//Function:extern "C" DLLEXPORT  int MdlMain
//Desc:Entry point of the program.
//******************************************************************************************/
extern "C" __declspec(dllexport)  int MdlMain
(
    int         argc,
    char        *argv[]
)
{
    AFX_MANAGE_STATE(AfxGetStaticModuleState());

    CDockableDialog* pDockable = new CDockableDialog(_T("Dockable Dialog"));
    if(NULL != pDockable)
    {
        pDockable->Create();
    }

    return SUCCESS;
}
```

CBNETDockableDialog 클래스는 SDK안에 있습니다.


---
* 2011.08.19\
> SDK안에 있는 Docking관련 소스 파일들을 프로젝트에 추가했다면
> nativewinmfc.lib 파일을 라이브러리 항목에 추가하지 마세요.
> nativewinmfc.lib 파일에 동일한 Docking관련 내용을 가지고 있습니다. 