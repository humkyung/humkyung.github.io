---
title: "which one we should select as model reference origin while converting 3D to 2D"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN, PDS]
---

제목을 쓰다 보니 길어졌는데요,\
간단히 말하자면 3D에서 2D로 변환시킬 때 3D의 기준 좌표로 어디를 선택하느냐는 것입니다.

지금 수행중인 도면 자동화 프로그램에서(PDS용) ISO 뷰에 대한 도면 작업을 하는 부분이 있습니다.

그래서 일반 뷰(TOP,BOTTOM,LEFT,RIGHT,FRONT,BACK)에서 처럼 3D 좌표를 2D로 좌표로 변환시키는 작업을 했습니다.\
그런데 원하는 결과가 나타나지 않고 그 위치가 조금 어긋나 있는 것이었습니다.

반나절을 헤멘 결과 그 원인을 찾았는데,\
View Reference 좌표는 PDS Hidden Drawing에서 얻었고, Model Reference 는 좌표는 PDS Database에서 뷰의 모델 min,max에서\
center를 구해서 model reference로 삼았습니다.

결과적으로 model reference에서 문제가 발생했습니다.\
사실 PDS Hidden Drawing에도 reference origin이라는 항목이 있는데 이 값이 일반 뷰에서는 PDS Database에서 계산한 값과 일치했습니다.

그런데 ISO 뷰에서는 그 값이 일치하지 않더군요.\
결론적으로 model reference 좌표는 PDS Hidden Drawing에서 구하는게 맞습니다.