---
title: "mdlLinkage_appendUsingDescr 사용하기"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN J]
---

mdlLinkage_appendUsingDescr을 사용하면 만들어진 Graphic Data에 여분의 사용자 데이터를 추가할수 있습니다.

아래 코드를 보시죠.

```c
LinkageHeader tLinkHdr;
int nStatus;
memset(tLinkHdr, '\0' , sizeof(LinkageHeader));
tLinkHdr.info       =0;
tLinkHdr.remote     =0;
tLinkHdr.modified   =0;
tLinkHdr.user       =1;
tLinkHdr.class      =0;
tLinkHdr.words;
tLinkHdr.primaryID  = SIGNATUREID_FDNPROJECT;
memset(elementInfo,'\0',sizeof(ElementInfo));
strncpy(elementInfo.name,element->name,64);
strncpy(elementInfo.site,element->site,64);
strncpy(elementInfo.zone,element->zone,64);
nStatus = mdlLinkage_appendUsingDescr(
    elemDescrPP,
    tLinkHdr,
    elementInfo,
    DATADEFID_ELEMENT_INFO, //  data def resource ID
    NULL,           //   conversion rules
    FALSE);
if(SUCCESS != nStatus)
{
    mdlDialog_dmsgsPrint("mdlLinkage_appendUsingDescr function error");
}
```

SIGNATUREID_FDNPROJECT은 사용자 데이터의 ID라고 생각하시면 되구요.\
DATADEFID_ELEMENT_INFO은 사용자 데이터 구조의 ID라 생각하시면 됩니다.\
이러한 사용자 데이터 구조는 리소스에 포함되어 컴파일 되어야 합니다.

따라서 프로그램 초기에 아래와 같은 코드를 포함하고 있어야 합니다.

```c
char *setP = NULL;
RscFileHandle rfHandle;
if (SUCCESS != mdlResource_openFile (rfHandle, NULL, TRUE))
{
    /* unload this application */
    mdlDialog_cmdNumberQueue (FALSE, CMD_MDL_UNLOAD, mdlSystem_getCurrTaskID(), TRUE);
    return ERROR;
}
mdlState_clear();
setP = mdlCExpression_initializeSet(    VISIBILITY_DIALOG_BOX |
                    VISIBILITY_CALCULATOR |
                    VISIBILITY_DEBUGGER,0,FALSE);
mdlDialog_publishComplexVariable(setP,"tagElementInfo"     ,"elementInfo"     ,elementInfo);
```

즉 리소스 파일을 오픈하여 사용자 데이터 구조의 정보를 구해야 합니다.

위 코드는 MSTN J에서 테스트했습니다.