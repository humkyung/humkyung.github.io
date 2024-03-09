---
title: "error C3861: 'toolSubsystem_fwrite': identifier not found"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM]
---

V8i용 프로그램을 개발할때 파일을 읽기 위해 fstream을 인클루드했을때 아래와 같은 에러를 뱉어 내었습니다.\
아마도 mdl 관련 헤더 파일에서 이 부분을 재정의를 한 것 같습니다.(왜 그렇게 했는지는 이해가 안 가네요...)\
![](2011-07-05-63.png)

단지 아래와 같이 fstream을 인클루드만 했을뿐인데 말이죠...
```cpp
#include <fstream>
#include <vector>
using namespace std;
// CDockableDialog dialog
IMPLEMENT_DYNAMIC(CDockableDialog, CBNETDockableDialog)
```