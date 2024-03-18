---
title: "Docking DialogBar 생성하기"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL]
---

간단한 Docking가능한 DialogBar를 생성하는 예제입니다.

mdl source , dialog box에 관련된 resource file , icon resource file로 구성되어 있습니다.

icon은 icon editor를 통해서 만들었습니다.

![](2011-07-05-12.jpg)
 
 ```c
#include "dtoolcmd.h"
#include "aDraw_PDSPick.h"
DialogBoxRsc TOOLBOXID_MAIN =  
{ 
     DIALOGATTR_TOOLBOXCOMMON, 
     0, 0, 
     NOHELP, MHELP, NOHOOK, NOPARENTID,  
     "", 
    { 
    { { 0, 0, 0, 0}, ToolBox, TOOLBOXID_PDSPickTools, ON, 0, "", ""}, 
    } 
};                                                       

DItem_ToolBoxRsc TOOLBOXID_PDSPickTools = 
{ 
     NOHELP, MHELPTOPIC, NOHOOK, NOARG, 0, "Pick Tools", 
    { 
    { { 0, 0, 0, 0}, IconCmd, ICONCMDID_PDSPick, ON, 0, "", ""}, 
    } 
}; 
/*----------------------------------------------------------------------+
|                                                                       |
|    
|                                                                       |
+----------------------------------------------------------------------*/
DItem_IconCmdRsc ICONCMDID_PDSPick = 
{ 
    NOHELP, OHELPTASKIDCMD, 0,  
    CMD_PICK_POINT, OTASKID, "Pick", 
    "", 
    { 
    }
} 
extendedAttributes 
{ { 
    {EXTATTR_FLYTEXT, "Pick a point"},
    {EXTATTR_BALLOON, "Pick a point"},
} };
```

여기서 ICONCMDID_PDSPick의 값이 Icon의 Resource ID와 같아야 Icon이 표시가 됩니다.\
CMD_PICK_POINT는 Icon을 눌렀을때 발생하는 Command 값입니다.

```c
 /*----------------------------------------------------------------------+
 |                                                                       |
 |   Include Files                                                       |
 |                                                                       |
 +----------------------------------------------------------------------*/
 #include
 #include
 #include
 #include
 #include
 #include
 #include
 #include
 #include
 #include

 #if defined (MSVERSION) && (MSVERSION >= 0x550)
 #include
 #include
 #include
 #include
 #include
 #include
 #include
 #include
 #include
 #include
 #endif

 #include "aDraw_PDSPick.h"
 #include "dtoolcmd.h"

 #pragma  Version 5:5:0

 #define MAX_PATH        256

 /*----------------------------------------------------------------------+
 |                                                                       |
 |   Private Global Variables                                            |
 |                                                                       |
 +----------------------------------------------------------------------*/
 Private char            *setP; 
 Private char            szIniFilePath[MAX_PATH + 1]; 
 Private char            szSection[MAX_PATH + 1] , szKey[MAX_PATH + 1]; 
 Private Dpoint3d        pointArray[10]; 

 /*----------------------------------------------------------------------+
 |                                                                       |
 |   Public Global Variables                                             |
 |                                                                       |
 +----------------------------------------------------------------------*/
 Public  DialogBox               *paletteDbP = NULL; 

 /*----------------------------------------------------------------------+
 |                                                                       |
 | name          PDSPick_reloadFunction                                  |
 |                                                                       |
 +----------------------------------------------------------------------*/
 Private void PDSPick_reloadFunction 
 (   
  void
  ) 
 { 
         DialogBox       *dbP=NULL; 

         if ((dbP = mdlDialog_open (NULL, TOOLBOXID_MAIN)) != NULL) 
         { 
                 if (mdlWindow_getDocked (dbP)) 
                 { 
                         /* docking requires that the application area be reorganized */
                         mdlWindow_organizeApplicationArea (); 
                 } 
         } 

         mdlCurrTrans_identity (); 
 } 

 /*----------------------------------------------------------------------+
 |                                                                       |
 | name          OnPickPoint                                             |
 |                                                                       |
 +----------------------------------------------------------------------*/
 Private void    OnPickPoint 
 ( 
 Dpoint3d    *pt, 
 int         view 
 ) 
 { 
         mdlDialog_openAlert("Pick point"); 
         mdlState_startDefaultCommand(); 
 } 

 /*----------------------------------------------------------------------+
 |                                                                       |
 | name          OnPickPoint                                             |
 |                                                                       |
 +----------------------------------------------------------------------*/
 Private void    OnPickDynamicPoint 
 ( 
 Dpoint3d    *pt, 
 int         view 
 ) 
 { 
         PDSPick_WriteDataPointForItem(pt->x , pt->y); 
         mdlState_startDefaultCommand(); 
 } 

 /*----------------------------------------------------------------------+
 |                                                                       |
 | name          getStartPoint                                           |
 |                                                                       |
 +----------------------------------------------------------------------*/
 Private void    getStartPoint 
 ( 
  Dpoint3d    *pt,      /* first point of leader */
  int         view      /* view number           */
  ) 
 { 
         char    terminatorCell[10]; 

         /* --- set current transform matrix to align with view --- */
         mdlCurrTrans_identity (); 
         mdlCurrTrans_rotateByView (view); 
         mdlCurrTrans_rotateByAngles (fc_zero, fc_zero, tcb->actangle*fc_piover180); 

         /* --- put points in terms of current coordinate system --- */
         mdlCurrTrans_invtransPointArray (&pointArray[0], pt, 1); 

         /* --- if terminator type is CELL then get current terminator cell --- */
         /*
         if (draftoolsParams.terminatorType == CELL)
         {
                 mdlParams_getActive (terminatorCell, ACTIVEPARAM_TERMINATOR);
                 if (terminatorCell[0])
                         createCellDescriptor (terminatorCell, &pointArray[0]);
         }
         */

         /* --- Set functions to handle datapoints, resets, and dynamics --- */
         mdlState_setFunction (STATE_DATAPOINT,          OnPickPoint); 
         mdlState_setFunction (STATE_COMPLEX_DYNAMICS,   OnPickDynamicPoint); 
         ///mdlState_setFunction (STATE_RESET,              restartCommand);

         /* --- display the correct prompt --- */
         /*
         if (mode == CALLOUT)
                 mdlOutput_rscPrintf (MSG_PROMPT, NULL, 0, PROMPT_CalloutPoint);
         else
                 mdlOutput_rscPrintf (MSG_PROMPT, NULL, 0, PROMPT_EndPoint);
         */
 } 

 /*----------------------------------------------------------------------+
 |                                                                       |
 | name          resetCommand                                            |
 |                                                                       |
 +----------------------------------------------------------------------*/
 Private void    resetCommand() 
 { 
         mdlState_clear (); 
 } 

 /*----------------------------------------------------------------------+
 |                                                                       |
 | name          cmdPickPoint                                            |
 |                                                                       |
 | author        BSI                                     10/93           |
 |                                                                       |
 +----------------------------------------------------------------------*/
 cmdName void    cmdPickPoint 
 ( 
 char    *unparsedP 
 ) 
 cmdNumber CMD_PICK_POINT 
 { 
         mdlState_startPrimitive (getStartPoint, resetCommand, 
                 0, 0); 
 } 

 /*----------------------------------------------------------------------+
 |                                                                       |
 | name          main                                                    |
 |                                                                       |
 +----------------------------------------------------------------------*/
 int main(int argc,char *argv[]) 
 { 
         char *setP = NULL; 
         RscFileHandle rfHandle; 
          
         mdlResource_openFile (&rfHandle, NULL, TRUE); 
          
         /*-------------------------------------------------------------------
         Load the application command table and resources
         -------------------------------------------------------------------*/
         if (mdlParse_loadCommandTable (NULL) == NULL) 
                 mdlOutput_rscPrintf (MSG_ERROR, NULL, 0, 4); 

         /* --- set ulooad and reload functions --- */
         mdlSystem_setFunction (SYSTEM_RELOAD_PROGRAM, PDSPick_reloadFunction); 

         ///mdlState_clear();
         ///if(3 == argc)
         { 
                 ///strcpy(szIniFilePath , argv[2]);
                         PDSPick_reloadFunction(); 
         /*
         else
         {
                 mdlDialog_openAlert("invalid parameter - setting file path is not setted.");
         }
         */

         return SUCCESS; 
}
```

PDSPick_reloadFunction 함수가 DialogBox를 생성합니다.

cmdPick 함수가 약간 특이한 형식을 가지고 있는데요,\
이게 DialogBox의 Icon을 눌렀을때 호출되는 함수입니다. CMD_PICK_ICON이란 값을 볼수 있는데, Resource쪽에도 같은 값이 있는 것을 알수가 있습니다.