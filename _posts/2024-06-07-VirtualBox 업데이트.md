---
title: VirtualBox 업데이트
categories:
  - IT
tags:
  - VirtualBox
use_math: true
---
기존 사용하고 있던 VirtualBox 7.0.10-158379에서 7.0.18-162988으로 업데이트를 하고 나서 실행하니 아래와 같은 오류가 발생했습니다.  

### ntcreatefile(\\device\\vboxdrvstub) failed: 0xc0000034

이 오류는 아래 방식으로 해결할 수 있습니다.  

1. 기존 VirtualBox를 삭제하고 컴퓨터를 재부팅합니다.
2. C:\Windows\System32\drivers\에서 남아 있는 VBox*.sys 파일을 삭제합니다.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj1Uzgr87pfIFzC8TfkCL4hGmbyGSXbbEDPpJcFCBMMmdzVDfp_AithU9FctC-_gJY2uR9XqiO6OsBz7_1TbKQ1Ra41Dg7_LLk1d73nH3ku7pwA0dWTriqrvvm6aVocsirK-V1T0Mj-lK-URabtkYO8ekMV-Ai5MTKpd3vxxaoe80HThLSsqzo_PWfbc58/s600/Pasted%20image%2020240607063828.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj1Uzgr87pfIFzC8TfkCL4hGmbyGSXbbEDPpJcFCBMMmdzVDfp_AithU9FctC-_gJY2uR9XqiO6OsBz7_1TbKQ1Ra41Dg7_LLk1d73nH3ku7pwA0dWTriqrvvm6aVocsirK-V1T0Mj-lK-URabtkYO8ekMV-Ai5MTKpd3vxxaoe80HThLSsqzo_PWfbc58/s514/Pasted%20image%2020240607063828.png)

4. 다시 컴퓨터를 재부팅합니다.
5. 관리자 권한으로 VirtualBox를 설치합니다.