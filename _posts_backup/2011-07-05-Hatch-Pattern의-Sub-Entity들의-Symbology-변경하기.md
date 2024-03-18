---
title: "Hatch Pattern의 Sub Entity들의 Symbology 변경하기"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN J]
---

Hatch Pattern을 생성한 뒤 Hatch Pattern으로 생성되는 Sub Entity들의 Sub Entity들을 변경하는 방식입니다.\
아래 코드는 V7(J)에서 테스트한 코드입니다.

```c
if(SUCCESS == mdlElmdscr_new(edP, NULL, newElement))
{
    mdlElement_setSymbology(edP, nColor, nWeight, nStyle);
    if(SUCCESS == mdlPattern_hatch(patternEdPP, edP, NULL, NULL, GetRadian(fAngle), 1.0 * unitVal, 0, FALSE, FALSE) )
    {
        ptr = patternEdPP;
        do
        {
            mdlElement_setSymbology((ptr->el), nColor, nWeight, nStyle);
        }while(ptr = ptr->h.next);
        mdlElement_setSymbology((patternEdPP)->el, nColor, nWeight, nStyle);
        mdlElmdscr_add (patternEdPP);
        mdlElmdscr_display (patternEdPP, 0, NORMALDRAW);
        mdlElmdscr_freeAll (patternEdPP);
        mdlElmdscr_freeAll (edP);
    }
    else    return FALSE;
}
```

```c
ptr = patternEdPP;
do
{
    mdlElement_setSymbology((ptr->el), nColor, nWeight, nStyle);
}while(ptr = ptr->h.next);
```

이 부분이 Sub Entity들의 Symbology를 변경하는 부분입니다.