---
title: "ProgressBar 표현"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM]
---

어떤 다소 시간이 걸리는 작업을 할때 사용자들을 멍~하니 기다리게 하는 것보다
ProgressBar를 표시하는 것이 효과적입니다.

예제)
열린 파일에서 현재 읽고 있는 요소대한 진행 상태를 표시하는 방법에 대해 알아보도록 하겠습니다.(즉 현재 몇번째 요소를 읽고 있는지 나타내는...)

* 화면에 표시할 다이얼로그 리소스 준비\
![](2011-08-22-1.png)
* 다이얼로그를 생성할 쓰레드 생성\
작업 쓰레드에서 다이얼로그를 생성하도록 합니다.\
여기서 하고 싶은 말 : mdlXXX류의 함수는 작업 쓰레드에서 제대로 작동하지 않을수 있으니... 주 쓰레드에서 호출해야 한다는 것입니다.

```cpp
/******************************************************************************
    @author     humkyung
    @date       2011-08-22
    @class
    @function   StatusThreadEntry
    @return     UINT
    @param      LPVOID  pVoid
    @brief
******************************************************************************/
UINT StatusThreadEntry(LPVOID pVoid)
{
    CWorkStatusDlg* pDlg = (CWorkStatusDlg*)(pVoid);
    if(pDlg)
    {
        InterlockedExchange((LONG*)(&(pDlg->m_bThreadRunning)) , TRUE);
        pDlg->DoModal();
    }
    
    return ERROR_SUCCESS;
}

extern "C" __declspec(dllexport) int __stdcall RevMISC(const CString &INI_FILE_PATH)
{
    AFX_MANAGE_STATE(AfxGetStaticModuleState());

    CWorkStatusDlg dlg;
    dlg.m_pThread = AfxBeginThread(StatusThreadEntry , &dlg , THREAD_PRIORITY_NORMAL , 0 , CREATE_SUSPENDED);
    if (NULL != dlg.m_pThread)
    {
        /// do something

               InterlockedExchange((LONG*)(&(dlg.m_bThreadRunning)) , FALSE);
           dlg.PostMessage(WM_COMMAND , IDOK);
    }

    return 0;
}
```
* 다이얼로그 상의 프로그래스바에 현재 진행 상태 표시