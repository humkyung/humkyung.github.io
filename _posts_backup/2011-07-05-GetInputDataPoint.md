---
title: "GetInputDataPoint"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL]
---

사용자 입력 데이터 포인터를 구해 파일로 저장하는 매크로 입니다.

```vb
Sub main 
    Dim point1          as MbePoint 
    Dim stat            as Integer 
    Dim view            as Integer 
    Dim ass             as String 

    MbeState.messages = 0

    Call MbeWritePrompt ("Select input data point") 
    ' wait for data or reset
    Call MbeGetInput (MBE_DataPointInput, MBE_ResetInput) 
    if MBE_Success = MbeState.getInputDataPoint (point1, view) then
            ass = Format$(point1.x , "#0.0#") & "," & Format$(point1.y , "#0.0#") & "," & Format$(point1.z , "#0.0#") 
            Open "c:\inputdatapoint.dat" For Output Access Write Lock Write As #1
                    Write #1,ass 
            Close
    end if  
    Call MbeWritePrompt ("finished") 
End Sub
```