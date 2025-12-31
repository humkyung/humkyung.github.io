---
title: "XM MDL Programming - #4(Element 탐색하기)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

이번에는 dgn 파일에 있는 element들을 찾는 방법을 알아보도록 합시다.

먼저 간단한 코드를 먼저 보시죠.

```cpp
int ScanFile(UShort* typeMask , constintmaskSize)
{
    intstatus = 0;
    intnElemCnt = 0;
    intnElemType;
    ULong elemAddr[50];

    ScanCriteria* pScanCrit = NULL;

    UShort usTypeMask[8];

    MSElement element;

    // Initialize the scan criteria
    pScanCrit = mdlScanCriteria_create();

    mdlScanCriteria_setReturnType(pScanCrit, MSSCANCRIT_RETURN_FILEPOS, FALSE, FALSE);

    memset(usTypeMask, 0, sizeof(usTypeMask));

    mdlScanCriteria_setElementTypeTest(pScanCrit , typeMask , maskSize);
    mdlScanCriteria_setModel (pScanCrit,mdlModelRef_getActive());

    mdlScanCriteria_setElementCategory (pScanCrit,ELEMENT_CATEGORY_GRAPHICS);

    do
    {
        intscanWords = sizeof(elemAddr) / sizeof(short);
        status = mdlScanCriteria_scan(pScanCrit, elemAddr, &scanWords, NULL);

        if( status == BAD_FILE || status == BAD_ELEMENT ) break;

        intnumAddr = scanWords / sizeof(short);
        for(inti=0; i < numAddr; i++)
        {
            if(mdlElement_read(&element, MASTERFILE, elemAddr[i]) == SUCCESS)
            {
                nElemCnt++;
                nElemType = mdlElement_getType(&element);
            }
        } //end for
    } while(status == BUFF_FULL);

    mdlScanCriteria_free(pScanCrit);

    return nElemCnt;
}
```

원리는 먼저 ScanCriteria 생성한 후에 탐색할 Element Type을 설정합니다.
그리고 난후 ScanCriteria로 탐색을 하면 설정한 Element Type만 탐색을 하게 됩니다. 또한 탐색한 Element의 file position을 돌려줍니다.

모든 프로그래밍에서도 다 그렇지만 생성한 ScanCriteria를 해제해 주면 됩니다.