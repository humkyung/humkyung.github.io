---
title: "XM MDL Programming - #9(메뉴 생성하기)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

dgnlib 이라는 파일을 가지고 툴바와 메뉴를 생성할 수 있습니다.

우선 Project와 User를 선택하여 해당 dgnlib 파일을 엽니다.\
![](2011-07-05-37.jpg)
![](2011-07-05-38.jpg)
 
Workspace --> Customize 메뉴로 갑니다.\
![](2011-07-05-39.jpg)
![](2011-07-05-40.jpg)
 
오른쪽 부분에서 마우스 오른쪽 클릭을 하여 New Menu와 New Menu Item을 통하여 메뉴를 생성합니다.
![](2011-07-05-41.jpg)

 
 메뉴를 생성했다면 메뉴를 선택했을 때 실행되는 루틴을 설정하는게 꼭 필요한데요,\
메뉴의 Properties 항목 중에서 Key-in 항목에서 실행하는 명령을 입력하면됩니다.
![](2011-07-05-42.jpg)


 
메뉴와 실행되는 명령이 서로 부합되지는 않지만 뭐~~ dgnlib 파일을 저장하고 나서 빠져 나갑니다.\
이제 dgn 파일을 오픈해 보면 우리가 방금 만든 메뉴가 기존의 메뉴에 추가되어 있는 것을 볼 수 있습니다.
![](2011-07-05-43.jpg)


 
앞서 우리가 만든 dgnlib 파일은 general Project 그리고 example User 일 때만 적용됩니다.