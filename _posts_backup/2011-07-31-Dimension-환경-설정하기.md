---
title: "Dimension 환경 설정하기"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN J, Dimension]
---

고객사로부터 아래와 같이 Dimension을 표기해 달라는 요청이 들어왔습니다.\
![](2011-07-05-64.png)


Dimension을 Dual로 표기해 달라는 것인데,\
상단에는 ft-inch로 하단에는 metric으로 표기해 달라는 것이었습니다.

이렇게 표기 가능하도록 MSTN J7의 Dimension 환경 설정을 해보도록 하겠습니다.

[Dimension Settings --> Units]\
![](2011-07-05-65.png)

1. Format을 <code style="color:red">AEC</code>로 선택합니다.
2. Primary Dimension 설정:
> Units을 Feet로 설정합니다.
3. Secondary Dimension 설정:
> Show Secondary Units를 체크합니다.\
> 이렇게 해야만 하단에 Dimension이 표기가 됩니다.\
> Units을 Millimeters로 설정합니다.\
> Label : 하단에 표기될 단위를 입력합니다. 입력하지 않으면 <code style="color:red">MM</code>로 표기됩니다.

이렇게 설정하고 나서도 상단의 Dimension 단위 표기가 우리가 원하던 것과 다를 수 있습니다.\
상단의 Dimension 단위 설정은 "Setting-->Design File-->Working Units"에서 하실 수 있습니다.\
![](2011-07-05-66.png)


Unit Names의 Master Units,Sub Units에서 원하는 단위를 입력하면 됩니다.

이렇게 하면 거의 원하는 Dimension 형식대로 표기할 수 있습니다.\
마지막으로 하단의 Dimension을 감싸는 []표기 입니다.\
이것을 Dimension Prefix,Suffix라고 하는데 이것은 "Dimension Settings-->Custom Symbols"에서 설정할 수 있습니다.\
![](2011-07-05-67.png)


이렇게 해서 원하는 형식대로 Dimension을 표기할 수 있습니다.

주의) 결과 이미지를 보시면 하단의 Dimension Text가 []사이의 가운데에 놓여있지 않는것을 알수 가 있습니다.\
이것은 하단의 Dimension에는 단위 표기를 하지 않도록 Label에 공백을 입력했기 때문입니다.(두번째 이미지 참조)

---
* 2011.08.02;
> Lower Suffix를 입력하지 않고 Label에 ]을 입력하면 Dimension 텍스트가 왼쪽으로 치우치지 않게 출력할 수 있습니다.