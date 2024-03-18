---
title: "PDS NOZZLE DATA 분석"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, PDS]
---

PDS에서 Nozzle은 Cell형식으로 만들어져 있습니다.

Nozzle을 찾기 위해서 이 Cell들 중에서 drms linkage의 user id가 22인 Cell을 찾습니다.\
일단 이 Cell을 Nozzle로 간주할수가 있습니다.

다음 attribute linkage는 Nozzle이 속한 Equipment의 관한 dmrs linkage입니다.\
또 다음의 attribute linkage는 그냥 무시합니다.

그 다음에 나타나는 attribute는 user data linkage로써 nozzle의 이름을 가지고 있습니다.\
이 user data linkage의 data 부분에서 첫 10 바이트를 nozzle 이름으로 구하면 됩니다.
![](2011-07-05-9.jpg)

또한 Nozzle의 여러 정보들은 Database의 22 , 23번 테이블에 담겨져 있습니다.\
partition no와 nozzle의 occurrence number로 nozzle의 정보를 구할 수 있습니다.