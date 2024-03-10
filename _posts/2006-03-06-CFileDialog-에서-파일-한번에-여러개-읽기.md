---
title: "[공유] CFileDialog 에서 파일 한번에 여러개 읽기.."
img_path: /assets/images/MFC/
categories: [MFC]
tags: [VC++, MFC]
---

출처 9992028 블로그 입니다!! | 구리구리\
원문 https://blog.naver.com/9992028/120020372939

* 파일다이얼로그 생성할때 옵션에 아래것 추가하고 ..
```
OFN_NOLONGNAMES | OFN_EXPLORER | OFN_ALLOWMULTISELECT
```

* 파일다이얼로그 클래스 dlg 의 멤버변수 아래처럼 set한다.

```cpp
CString strFileName;

dlg.m_ofn.nMaxFile = 2048;
dlg.m_ofn.lpstrFile = strFileName.GetBuffer(2048);
```

* 여러개의 파일 읽을때는 POSITION을 이용한다.

```cpp
POSITION pos = dlg.GetStartPosition();
while( pos != NULL )
{
    CString strFile = dlg.GetNextPathName(pos);
    // do something
}
```