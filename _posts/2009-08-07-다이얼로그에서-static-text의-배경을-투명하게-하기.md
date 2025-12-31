---
title: "다이얼로그에서 static text의 배경을 투명하게 하기"
comments: true 
img_path: /assets/images/MFC/
categories: [MFC]
tags: [MFC]
---

다이얼로그에서 사용하는 static text의 배경색을 투명하게 하는 방법입니다.

다이얼로그의 OnCtlColor를 아래와 같이 재정의합니다.
```cpp
HBRUSH COutstandingOptionDlg::OnCtlColor(CDC* pDC, CWnd* pWnd, UINT nCtlColor)
{
    HBRUSH hbr;

    const UINT nID = pWnd->GetDlgCtrlID();
    if(nCtlColor == CTLCOLOR_STATIC)
    {
        pDC->SetBkMode(TRANSPARENT); /// 배경을 투명하게
        hbr = (HBRUSH)::GetStockObject(NULL_BRUSH);
    }
    else
    {
        hbr = CDialog::OnCtlColor(pDC, pWnd, nCtlColor);
    }

    return hbr;
}
```

이것으로 투명한 static text를 만들수 있습니다.

다이얼로그의 배경으로 이미지를 넣었는데...

![](2009-08-07-1.jpg) 

왼쪽 부분은 static text의 배경을 투명하게 하지 않은 것이고,

오른쪽 부분은 배경으로 투명하게 한것입니다.

오른쪽의 것이 훨씬 보기 좋죠?