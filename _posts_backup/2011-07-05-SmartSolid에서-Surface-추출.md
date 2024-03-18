---
title: "SmartSolid에서 Surface 추출"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM, SmartSolid]
---

아래의 코드를 이용해서 SmartSolid에서 Surface를 추출할수 있습니다.

```cpp
if(mdlKISolid_isSmartElement(pElmDescr , MASTERFILE , filePos))
{
    MSElementDescrP destP = NULL;

    mdlKISolid_beginCurrTrans(MASTERFILE);

    // SmartSolid를 suface 리스트를 추출
    // destP에 추출한 surface 리스트가 담겨 있습니다.
    mdlKISolid_getSurfaceElements(&destP , pElmDescr , MASTERFILE , NULL);
    mdlKISolid_endCurrTrans();

    WriteElementDescr(oFile , pDgnModelRef , destP , filePos , dUOR , DGNType);
            
    mdlElmdscr_freeAll (&destP);
}
```