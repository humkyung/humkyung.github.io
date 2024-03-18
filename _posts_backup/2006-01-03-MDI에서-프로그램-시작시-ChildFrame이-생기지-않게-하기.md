---
title: "MDI에서 프로그램 시작시 ChildFrame이 생기지 않게 하기"
categories: [MFC]
tags: [MFC]
---

방법은 간단합니다.


xxxApp 클래스의 InitInstance()함수에서
```cpp
// Parse command line for standard shell commands, DDE, file open
CCommandLineInfo cmdInfo;
cmdInfo.m_nShellCommand = CCommandLineInfo::FileNothing; <--/// 추가 되는 부분
ParseCommandLine(cmdInfo);
```