---
title: "mdlView_hiddenLineRemoval2의 preFunction에 대해서..."
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL]
---

mdlView_hiddenLineRemoval2을 사용할때 첫번째 인자가 preFunction을 가르키는 함수 포인터이다.

이 preFunction이 하는 기능은 hidden 처리를 하는 과정에 앞서 현재 Active된 모델의 각 element들에 대해서

hidden 처리에 포함시킬지 여부를 결정한다.

이 preFunction 부분이 V7에서 XM으로 넘어오는 과정에서 약간 변경이 되었는데,

element들에 대한 정보는 preFunction의 첫번째 인자인 MSElementDescr *edP에서 구할 수 있다.

아래 코드는 XM환경에서 reference된 element의 모델 이름등을 구하는 루틴입니다.
```c
Private int preFunction
(
    MSElementDescr       *edP,                /* => element to be processed */
    ViewInfoP          elementInfoP
)
{
    int lineNo;
    char             modelName[256];
    char             modelDescription[256];
    char             modelLogical[256];
    DgnModelRefP    modelRef;
    StatusInt res;
    ULong filePos;
        if(mdlModelRef_isReference(edP->h.dgnModelRef))
        {
            mdlRefFile_getParameters(modelName,REFERENCE_FILENAME,edP->h.dgnModelRef);
            mdlRefFile_getParameters(modelDescription,REFERENCE_DESCRIPTION,edP->h.dgnModelRef);
            mdlRefFile_getParameters(modelLogical,REFERENCE_LOGICAL,edP->h.dgnModelRef);
            fprintf(fp , "modelName = %s\r\n",modelName);
            fprintf(fp , "modelDesc = %s\r\n",modelDescription);
            fprintf(fp , "modelLogi = %s\r\n",modelLogical);
        }
    return SUCCESS;
}
```