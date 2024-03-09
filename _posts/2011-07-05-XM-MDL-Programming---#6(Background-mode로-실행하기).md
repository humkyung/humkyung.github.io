---
title: "XM MDL Programming - #6(Background mode로 실행하기)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

ARX에서도 AutoCAD application을 활성화(?)시키지 않고 작업을 수행할수 있듯이,\
MDL 프로그램밍에서 그렇게 유사하게 작업을 수행할수 있습니다.

application이 Background mode로 실행되고 있는지 여부는 Entry point 함수의 두번째 인자를 검사함으로써 알수 있습니다.\
두번째 인자가 "MS_INITAPPS" 이면 Background mode로 실행되고 있는 것입니다.

그럼 어떻게 Background mode로 application을 실행시킬수 있을까요?

-waoption을 사용해서 application을 Background mode로 실행시킬수 있습니다.

예를 들면,\
```sh
"C:\Program Files\Bentley\MicroStation\ustation.exe" -waSample7.ma
```

여기서 Sample7.ma가 Background로 실행시키고자 하는 application 이름입니다.