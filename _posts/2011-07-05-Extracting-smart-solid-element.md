---
title: "Extracting smart solid element"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM]
---

```c
MSElementDescrP bodyToElements
(
KIBODY* pBody,        // =>
MSElementP pTemplate, // => can be NULL
int             nIsoLines    // =>
)
{
    MSElementDescrP     pNewEd = NULL;
           if (NULL == pBody)
                    return NULL;

    mdlKISolid_beginCurrTrans (ACTIVEMODEL);      
    mdlKISolid_bodyToElements (&pNewEd, pBody, TRUE, nIsoLines, pTemplate, ACTIVEMODEL);
    mdlKISolid_endCurrTrans ();

    return pNewEd;
}
```

아직 테스트하지 않았습니다. 테스트가 필요합니다.

---
- 2011.07.04\
kisolid.dll를 library에 추가해야 합니다.\
![](2011-07-05-52.png)
