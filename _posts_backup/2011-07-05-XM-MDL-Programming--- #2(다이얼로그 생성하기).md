---
title: "XM MDL Programming - #2(다이얼로그 생성하기)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

이번에는 다이얼로그를 생성하는 방법을 알아봅시다.

V7에서는 다이얼로그 하나 생성하기가 어려웠었는데,

XM 이후부터는 MFC 다이얼로그를 상속해서 사용하니까 MFC에 익숙한 사람은 아무 어려움 없이 사용할수 있습니다.

한 마디로 쉬워요.

아시다시피 모달/모달리스 다이얼로그가 있는데 모달 보다는 모달리스 다이얼로그가 유용하게 사용됩니다.

다이얼로그가 실행되어 있는 동안에 MSTN으로 왔다 갔다 하면서 작업을 해야 하니까요.(그리고 모달 다이얼로그는 그냥 DoModal() 함수를 호출하면 되니까 별로 할것도 없어요)

1. MS Visual Studio에서 리소스에서 다이얼로그를 하나 만듭니다.
> 여기서 조금 이상한데요. 모달리스 다이얼로그를 만들기 위해서는,
> Dialog Frame을 NONE으로 Style을 Child로 설정해야 한다고 합니다.

2. 다이얼로그와 대응하는 클래스를 하나 생성합니다.(이때 CDialog를 상속하도록 합니다.)
3. 생성한 클래스에서 부모 클래스를 첨부한 클래스로 변경합니다.
4. 클래스 인스턴스를 하나 생성합니다.
5. 인스턴스에서 Create()함수를 호출하여 모달리스 다이얼로그를 생성하면 됩니다.

```cpp
CBasicAppDlg* pDlg = new CBasicAppDlg("Basic Dialogbased MDL");
if(pDlg) pDlg->Create();
```

아주 쉽죠~~~
![](2011-07-05-15.jpg)