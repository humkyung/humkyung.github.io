---
title: "XM MDL Programming - #5(Element 생성하기)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

이번에는 간단히 예제로 Line과 Text를 생성하는 방법에 대해 알아보도록 합시다.

다른 Element들에 대해서는 생성하는 함수만 알면 아래의 루틴대로 하면 아무 어려움 없이 원하는 Element들을 생성할수 있습니다.\
루틴이라고 해봤자 생성하는 함수로 원하는 Element를 생성한 후에 Property를 설정하고 add하는 것 밖에 없습니다.

우선 간단한 다이얼로를 만든 뒤에 생성할 Element의 Type을 설정하는 ComboBox를 추가합니다.\
그리고 Place 버튼을 누르면 Element를 생성하는 것으로 하죠.\
![](2011-07-05-30.jpg)


자 그럼 Place 버튼의 Callback 함수를 보도록 하죠.
```cpp
void CModelessDlg::OnBnClickedBtnPlace()
{
    CMStationDialog::UpdateData(TRUE);
    startElementPlacement(this);
}
```
아래 startElementPlacement 함수를 호출합니다.

```cpp
void startElementPlacement(CModelessDlg* pDlg)
{
    g_pDlg = pDlg;
    CString csElement;
    int nIndex = g_pDlg->m_cbCtrlElemType.GetCurSel();
    if(nIndex != -1)
    {
        g_pDlg->m_cbCtrlElemType.GetLBText(nIndex,csElement);
        if(csElement.CompareNoCase("Line") == 0)
        {
            startLinePlacement();
        }
        else if(csElement.CompareNoCase("Text") == 0)
        {
            mdlState_setFunction (STATE_DATAPOINT, placeText);
            mdlState_setFunction (STATE_RESET, resetAction);
            mdlState_dynamicUpdate (dynamicTextDisplay, FALSE);
        }
    }
}
```

그럼 startLinePlacement 함수를 한번 보도록 할까요?

```cpp
void startLinePlacement()
{
    mdlState_startPrimitive (firstPoint, NULL, NULL, NULL);
    mdlOutput_printf(MSG_PROMPT,"Line Placement > Enter first point");
}
```

mdlState_startPrimitive 함수를 호출하는 것을 볼수 있습니다.\
mdlState_startPrimitive 함수는 Element를 생성할 때 호출하는 함수라고 기억하시면 됩니다.\
첫번째 인자로 함수 포인터를 넘겨주는데요, 사용자가 사용자가 마우스 왼쪽 버튼을 클릭했을때 호출되는 함수입니다.\
(마우스 오른쪽 버튼은 취소 기능입니다.)
```cpp
/***************************************************************************************** 
//Function : firstPoint(Dpoint3d *pntP,int view) 
//Desc : Start point of Line element
//Return : none 
//****************************************************************************************/ 
void firstPoint(Dpoint3d *pntP,intview) 
{ 
    MSElementDescr* pDescr = NULL; 

    g_dPts[FIRST_POINT]=*pntP; 
    
    mdlState_setFunction (STATE_DATAPOINT, secondPoint); 
    mdlState_setFunction (STATE_RESET, resetAction); 
    mdlState_dynamicUpdate (showLineDynamically, FALSE); 
    mdlOutput_printf(MSG_PROMPT,"Line Placement > Enter second point"); 
} 
```

위 함수는 사용자가 첫번째 왼쪽 마우스 버튼을 클릭했을 때 호출되는 함수이고(인자로 Dpoint3d*와 view number를 가짐),\
함수 내용을 보면 mdlState_setFunction을 사용하여 STATE_DATAPOINT , STATE_RESET에 해당하는 함수를\
설정해주는 것을 알수 있습니다.\
STATE_DATAPOINT에 설정된 함수는 사용자가 왼쪽 마우스 버튼을 클릭했을 때 호출되는 함수이고,\
STATE_RESET에 설정된 함수는 사용자가 오른쪽 마우스 버튼을 클릭했을 때 호출되는 함수입니다.\
mdlState_dynamicUpdate함수는 그 이름에서 풍기듯이 동적으로 업데이트 해주는 함수입니다.\
(RubberBand와 비슷한 기능을 구현하는데 사용하는 함수라고 생각하시면 될것 같네요.)
```cpp
/***************************************************************************************** 
//Function : secondPoint(Dpoint3d *pntP,int view)  
//Desc : Second point of Line element
//Return : none 
//****************************************************************************************/ 
void secondPoint(Dpoint3d *pntP,intview) 
{ 
    MSElement elm; 
    g_dPts[2] = *pntP; 
    
    // Create line element 
    mdlLine_create(&elm, NULL, g_dPts); 
    mdlElement_add(&elm); 
    mdlElement_display(&elm,NORMALDRAW); 
} 
``` 
mdlLine_create함수를 통해서 Line을 하나 생성한 후에, mdlElement_add 함수를 통해서 생성한 Element를 파일에 추가합니다.\
그리고나서 mdlElement_display함수를 사용해서 화면에 표시하도록 합니다.
 
이 함수들이 Element를 생성하는 가장 핵심이 되는 함수 입니다.
```cpp 
/***************************************************************************************** 
//Function : showLinesDynamically(DPoint3d *pntP,int view) 
//Desc : Show Line element dynamically
//Return : none
//****************************************************************************************/ 
void showLineDynamically(DPoint3d *pntP,intview) 
{ 
    MSElement elm; 
    // Store second point 
    g_dPts[SECOND_POINT] = *pntP; 
    mdlLine_create(&elm, NULL, g_dPts); 
    mdlElement_display(&elm,TEMPDRAW); 
} 
```
 
이 함수는 마우스가 움직일때마다 호출되는 함수인데요,\
마우스 포인터를 가지고 와서 Line을 하나 생성한 후에 화면에 표시합니다.\
여기서는 생성한 Element를 파일에 add하지 않고 그리고 TEMPDRAW에 화면에 표시한다는 것을 주의하시면 됩니다.
 
```cpp
void resetAction() 
{ 
    mdlState_clear(); 
    mdlState_startDefaultCommand(); 
} 
```

Reset함수입니다. State Machine의 상태를 클리어하고, Default Command를 실행합니다.\
위에서 본 루틴들은 아래와 같은 State Machine(컴파일러 이론때 배운것 같은데)의 흐름을 따릅니다.\
![](2011-07-05-31.jpg)