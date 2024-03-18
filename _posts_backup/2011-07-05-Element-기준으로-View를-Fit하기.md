---
title: "Element 기준으로 View를 Fit하기"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM]
---

아래 예제 코드를 참고 하시기 바랍니다.

```cpp
ret = mdlElement_read (&mseFeat, MASTERFILE, filePosP);
if (SUCCESS == ret)
{
    if (SUCCESS == mdlElement_extractRange (&dvVec, &mseFeat))
    {
        memset (&options, 0, sizeof (FitViewOptions));
        if (SUCCESS == mdlView_fitViewToRange (&dvVec.org, &dvVec.end, &options, 0))
        {
```