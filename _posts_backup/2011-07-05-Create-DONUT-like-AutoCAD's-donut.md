---
title: "Create DONUT like AutoCAD's donut"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN J]
---

AutoCAD에서의 Donut과 유사하게 MSTN J에서 Donut을 만드는 함수입니다.

함수 분석은 그리 어렵지 않구요.\
간단히 설명하자면 두개의 Ellipse를 생성한 다음에 큰 Ellipse에서 작은 Ellipse을 뺀 나머지 부분을 생성한 후 저장하면 됩니다.

```c
//! get difference pattern between two patterns
mdlElmdscr_differenceShapes(&patternEdPP, NULL, OutpatternEdPP, InpatternEdPP , 0);
```

자 그럼 코드를 볼까요...
```c
/**
@brief create donut
@author HumKyung.Baek
@date ????.??.??
@return boolean
*/
Private boolean Draw_Donut(floatfInsideDia, floatfOutsideDia, Dpoint3d *ptCenter, intnColor, intnLayer)
{
    MSElementUnion newElement, newInElement, newOutElement;
    inti, stat;
    intnFillmode = 1;
    intnWeight, nStyle;
    MSElementDescr *OutpatternEdPP = NULL, *InpatternEdPP = NULL, *patternEdPP = NULL;

    doubleunitVal = tcb->uorpersub;

    ptCenter->x = ptCenter->x * unitVal;
    ptCenter->y = ptCenter->y * unitVal;
    ptCenter->z = ptCenter->z * unitVal;

    stat = mdlEllipse_create(&newOutElement, NULL, ptCenter, fOutsideDia*unitVal, fOutsideDia*unitVal, NULL, nFillmode);
    if(stat != SUCCESS)
    {
        PrintError("Error creating graphic element!");
        returnFALSE;
    }

    mdlElement_setSymbology(&newOutElement, &nColor, NULL, NULL);
    mdlElement_setProperties(&newOutElement , &(nLayer) , NULL, NULL, NULL, NULL, NULL, NULL, NULL);

    if(fInsideDia > 0.0)
    {
        stat = mdlEllipse_create(&newInElement, NULL, ptCenter, fInsideDia*unitVal, fInsideDia*unitVal, NULL, nFillmode);
        if(stat != SUCCESS)
        {
            PrintError("Error creating graphic element!");
            returnFALSE;
        }

        mdlElement_setSymbology(&newInElement, &nColor, NULL, NULL);
        mdlElement_setProperties(&newInElement , &(nLayer) , NULL, NULL, NULL, NULL, NULL, NULL, NULL);

        mdlElement_display(&newInElement, NORMALDRAW);

        mdlElmdscr_new (&OutpatternEdPP, NULL, &newOutElement);
        mdlElmdscr_new (&InpatternEdPP, NULL, &newInElement);

        //! get difference pattern between two patterns
        mdlElmdscr_differenceShapes(&patternEdPP, NULL, OutpatternEdPP, InpatternEdPP , 0);
        mdlElmdscr_display(patternEdPP, 0, NORMALDRAW);
        mdlElmdscr_add (patternEdPP);

        //! free mstn element descriptions
        mdlElmdscr_freeAll(&patternEdPP);
        mdlElmdscr_freeAll(&InpatternEdPP);
        mdlElmdscr_freeAll(&OutpatternEdPP);
    }
    else
    {
        mdlElement_display(&newOutElement, NORMALDRAW);
        stat = mdlElement_add(&newOutElement);
        if(stat == 0)
        {
            PrintError("Error adding graphic element!");
            returnFALSE;
        }
    }

    returnTRUE;
}
```

아래는 샘플 output 이미지입니다.
![](2011-07-05-45.jpg)