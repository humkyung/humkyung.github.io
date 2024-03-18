---
title: "MSTN XM VBA - Lession3(요소 생성하기)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM, VBA]
---

VBA 교육은 하지 않는 것으로 결정이 났습니다.\
앞으로 VBA 관련 업데이트는 자주 없을것 같습니다.

자 이제 LineString을 그리는 매크로를 작성해 보도록 합시다.\
전체 소스는 아래와 같습니다.

```vb
Sub Macro1()
    Dim startPoint As Point3d
    Dim point As Point3d, point2 As Point3d
   
    'Start a command    CadInputQueue.SendCommand "PLACE SMARTLINE "
   
    'Coordinates are in master units
    startPoint.X = 7.316122
    startPoint.Y = -4.865692
    startPoint.Z = 0#
   
    'Send a data point to the current command
    point = startPoint
    CadInputQueue.SendDataPoint point, 1
   
    'Send a data point to the current command
    point.X = startPoint.X + 2.48087
    point.Y = startPoint.Y + 3.0765
    point.Z = startPoint.Z
    CadInputQueue.SendDataPoint point, 1
   
    'Send a data point to the current command
    point.X = startPoint.X + 7.6503
    point.Y = startPoint.Y + 1.9341
    point.Z = startPoint.Z
    CadInputQueue.SendDataPoint point, 1
   
    'Send a reset to the current command
    CadInputQueue.SendReset
   
    CommandState.StartDefaultCommand
End Sub
```

PLACE SMART 이라는 command를 이용하여 LineString을 생성하였습니다.

매크로를 끝내기 전에 StartDefaultCommand 명령을 통해서 CommandState 머신을 초기화 시켜줍니다.\
![](2011-07-05-26.jpg)