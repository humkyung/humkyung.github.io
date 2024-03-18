---
title: "XM MDL Programming - #3(Command 사용하기)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

이번에는 Command를 사용하는 방법에 대해서 알아보도록 하죠.

일단 먼저 MSTN의 리소스 파일을 이용하여 Command 구조를 선언합니다. 이것을 컴파일하면 .ma 파일이 생성됩니다.\
![](2011-07-05-27.jpg)


CT_BASIC이 최상위 Command Table 이름이고, CT_DELETE라는 하위 Command Table을 필요(REQ)로 합니다.\
CT_DELETE라는 Table은 CT_BASICAPP에서 상속(INHERIT)을 받고 더 이상의 하위 Command Table은 필요로 하지 않습니다.

.mke 파일을 잠깐 살펴보면...
```sh
# Create needed output directories if they don't exist
$(rscOutDir)$(tstdir) : $(rscOutDir)$(tstdir)        

$(maOutDir)$(tstdir)  : $(maOutDir)$(tstdir)

rscCompIncs + -i$(hdrOutDir) -i$(baseDir)inc/

appRscs = $(rscOutDir)$(appName).rsc

$(incDir)$(appName)Cmd.h    : $(rsrcInc)$(appName)Cmd.r

$(rscOutDir)$(appName)Cmd.rsc    : $(rsrcInc)$(appName)Cmd.r

$(rscOutDir)$(appName).rsc    : $(rsrcInc)$(appName).r

rscLinkObjs  =  $(rscOutDir)$(appName).rsc\
$(rscOutDir)$(appName)Cmd.rsc
```

여기서 10번째 줄을 주의해서 살펴볼 필요가 있습니다.\
Command를 정보를 가지고 있는 리소스 파일에서 *.h 파일을 생성시키는 부분입니다.

이 *.h 파일은 아래에서 사용할 Command Number를 가지고 있습니다.

아래는 *.h 파일의 내용입니다.
```c
#define CMD_MYDELETE                            0x01000000  /* MANIPULATION */ 
#define CMD_MYDELETE_ELEMENT                    0x01010000  /* MANIPULATION */
```

실행은 MSTN의 Key-in UI에서 'MYDELETE ELEMENT' 입력을 하면 이것과 연결된 Command가 실행이 됩니다.

실제적인 각 Command의 정의는 .dll에 포함이 됩니다.\
대부분의 프로그램에서 초기에 Command를 등록시켜 주겠죠?\
MDL Programming에서도 이와 다를바가 없습니다.

```cpp
if(SUCCESS != mdlSystem_registerCommandNumbers(commandNumbers))
{
    AfxMessageBox("Fail to register command numbers");
    return 1;
}
if(NULL== mdlParse_loadCommandTable(NULL))
{
    AfxMessageBox("Fail to load command table");
    return 1;
}
```

mdlSystem_registerCommandNumbers 함수를 통해서 Command를 등록합니다.\
인자로 MdlCommandNumber 타입의 배열을 받습니다.\
MdlCommandNumber는 Command Number와 실행시 호출되는 함수 포인터를 가지고 있습니다.

등록을 성곡적으로 마쳤다면 이제 실제 우리가 앞서 MSTN 리소스 파일에서 정의한 Command Table을\
mdlParse_loadCommandTable 함수를 호출하여 로딩합니다.

```cpp
voidMyDeleteElement(CHAR* unparsed)
{
    AfxMessageBox("delete element");
}

Private MdlCommandNumber commandNumbers[]=
{
    {MyDeleteElement, CMD_MYDELETE_ELEMENT},
    0
};
```

commandNumbers에서 CMD_MYDELETE_ELEMENT에 대응하는 함수 MyDeleteElement를 선언합니다.\
즉 CMD_MYDELETE_ELEMENT라는 Command가 호출되었을 때 MyDeleteElement 함수가 호출된다는 의미입니다.

자 그럼 CMD_MYDELETE_ELEMENT라는 번호는 어디에서 왔을까요?\
우리가 앞서 MSTN 리소스 파일에서 Command Table을 정의했습니다.\
이것을 컴파일을 하면 .ma 파일이 생성되는데 이때 실제 프로그램에서 사용할 Command Number가 생성됩니다.\
즉 이 Number를 Command Number Table에 사용하면 됩니다.\
![](2011-07-05-28.jpg)
![](2011-07-05-29.jpg)