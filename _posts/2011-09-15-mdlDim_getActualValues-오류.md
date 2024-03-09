---
title: "mdlDim_getActualValues 오류"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM]
---

Dimension의 텍스트를 읽을때 텍스트가 자동으로 계산되어 표시되는 경우는 mdlText_extract 함수를 통하여 읽었을때 *로 읽힙니다.

이럴때 mdlDim_getActualValues 함수를 통하여 실제 값을 구할 수 있습니다.\
하지만 이 함수가 완전하지 않은지 가끔씩 에러가 발생합니다.\
원인과 해결 방법을 알고 계신 분은 좀 알려 주세요...

```cpp
double pdValues[256] = {0,};
f (SUCCESS == mdlDim_getActualValues(&(element->el) , pdValues))
{
    m_sTextString.Format (_T("%.4f") , (pdValues[0] / uor));
}
```