---
title: "WM_GETDLGCODE"
img_path: /assets/images/MFC/
categories: [MFC]
tags: [MFC]
---

![](2007-06-09-1.jpg)

다이얼로그에 위와 같은 에디터 컨트롤을 놓았습니다.
 
일반적인 방향키는 제대로 먹었으나 엔터키가 작동하지 않았습니다.
 
그래서 여기저기 찾아보니 다이얼로그 위에 놓이는 컨트롤에 WM_GETDLGCODE처리하는
 
메서드를 오버라이드해서 DLGC_WANTALLKEYS를 리턴하면 모든 키들을 처리할 수 있습니다.

```cpp 
//{{AFX_MSG(CNoteEdit)
 afx_msg UINT OnGetDlgCode();
 //}}AFX_MSG
 
BEGIN_MESSAGE_MAP(CNoteEdit, CEdit)
 //{{AFX_MSG_MAP(CNoteEdit)
 ON_WM_GETDLGCODE()
 //}}AFX_MSG_MAP
END_MESSAGE_MAP()
 
UINT CNoteEdit::OnGetDlgCode()
{
    return DLGC_WANTALLKEYS;
}
```