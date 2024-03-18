---
title: "mdlLinkage_appendUsingDescr 오류"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN J]
---

mdlLinkage_appendUsingDescr 호출 실패 때문에 미치겠습니다.

다른 프로젝트와 똑 같이 했는데 왜 실패하는지?

-------------------------------------------------------------------------------------------------------------
```c
mdlCell_create(&groupCell, pToken1->buf[2], NULL, FALSE);
mdlElmdscr_new(&chainDscrP,NULL,&groupCell);

addUserData(&chainDscrP , filePos); //! mdlLinkage_appendUsingDescr 호출

filePos = mdlElmdscr_add(chainDscrP);

Private int addUserData( MSElementDescr **elP , ULong filePos )
{
    int status;
    char cMsg[100];
    char linkString[MAXFILELENGTH];
    LinkageHeader linkHdr;


    memset(&linkHdr, '\0' , sizeof(LinkageHeader));
    linkHdr.info =0;
    linkHdr.remote =0;
    linkHdr.modified =0;
    linkHdr.user =1;
    linkHdr.class =0;
    linkHdr.words;
    linkHdr.primaryID = 901;


    memset(&linkInfo , '\0' , sizeof(LinkInfo));
    strcpy(linkInfo.tag_Name1 , "hello");
    status = mdlLinkage_appendUsingDescr(
    elP,
    &linkHdr,
    &linkInfo,
    RSCID_DataDef_Link,
    NULL,
    FALSE);


    if (status == SUCCESS )
    {
    }
    else
    {
        PrintError ("\nError adding user data!");
    }

    return (status == SUCCESS) ? MODIFY_STATUS_REPLACE : MODIFY_STATUS_ABORT;
}
```