---
title: "Microstation J와 file size 32MB"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN J]
---

Microstation J까지의 버전에서 DGN file이 32MB가 넘어가면 문제가 발생한다고 합니다.

주의하세요!!!

<code style="color:red">mdlSystem_compressDgnFile</code>함수를 호출하면 Undo같은 기능을 위해 저장하고 있는 내용을 지워 파일 크기를 줄일 수가 있습니다.

J가 워낙 오래된 프로그램이라 파일 크기 제한은 현재 상황과 맞지 않습니다.\
PDS사용자들은 어쩔수 없이 사용할수 밖에 없구요.