---
title: "Microstation J를 VB에서 호출하기"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL]
---

먼저 VB에서 호출하기 위해서는 레지스트리에 Microstation.Application의 PROGID가 아래와 같이 존재하여야 합니다.\
![](2011-07-05-6.jpg)

VB에서는 지금까지 해오던 대로 GetObject를 호출하여 Microstation J Application을 잡으면 됩니다.\
![](2011-07-05-7.jpg)

여기서 msApp의 Visible을 활성화 시키지 않으면 msApp에 명령어를 보내기 위해 사용하는 MbeSendCommand가 제대로 실행되지 않습니다. <code style="color:red">--> 주의</code>

위 코드는 msApp를 생성해서 명령행으로 주어지는 dgn 파일을 오픈하는 코드입니다.

위와 유사한 코드를 Python에서 하려고 시도했었는데, Python에서는 msApp Object를 제대로 가져오지 못하고 에러가 발생하더군요.\
이런면을 보면 VB가 참 잘 만들어 졌다고 보여집니다.

---
<code style="color:green">
위의 코드는 수정되어야 합니다.<br>
MSTN J 상위 버젼이 설치되어 있는 경우에 위의 코드는 제대로 작동하지 않습니다.<br>
그래서 트릭으로 MSTN J를 Shell 함수를 통해서 강제로 실행 시킨 후에<br>
GetObject("","Microstation.Application")을 통해서 Microstation Object를 가져올 수 있습니다.<br>
</code>

---
<code style="color:red">
이것 마저도 되지 않을때 MSTN J를 다시 설치하시면 될것입니다.
</code>