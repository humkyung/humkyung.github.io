---
title: "memory allocation의 비용"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN J]
---

메모리 할당/해제에 당연히 어느 정도의 비용이 든다고는 알고 있었지만,

V7에서의 눈에 띄는 성능 저하는 메모리 할당/해제의 문제라 생각하지 못할 정도였다.

몇백개의 line,text들을 생성하는데 생성하는 것을 눈으로 확인할수 있을 정도로 속도가 느렸습니다.

메모리 할당/해제 대신에 배열을 사용하니,

정말 눈깜짝할 정도의 시간에 모든 line,text의 생성이 완료가 되었습니다.

아마도 mdl compiler의 메모리 할당/해제에 문제가 있는게 아닌가 합니다.