---
title: "FrameWork Data 분석"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL]
---

아래는 FrameWork으로 생성한 칼럼의 user linkage의 data 부분을 덤프한 내용입니다.
![](2011-07-05-10.jpg)


F10-3d 부분이 칼럼의 이름이 됩니다.

따라서 user data linkage의 data 부분에서 12 바이트 떨어진 곳에서 16 바이트를 읽어내면

칼럼의 이름을 구할 수 있습니다.