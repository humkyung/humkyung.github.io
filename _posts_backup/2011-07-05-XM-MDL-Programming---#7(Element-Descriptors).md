---
title: "XM MDL Programming - #7(Element Descriptors)"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MDL XM]
---

이 부분은 본래 MDL Programming하기 전에 반드시 알아야만 하는 부분입니다.(뒷늦게 올리게 되었네요)

프로그래밍에서 주로 하는 일은 Element들을 다루는 일일 것입니다.\
따라서 이 Element들이 어떻게 저장되어 있는지를 꼭 알아야만 합니다.(ARX를 시작하기 전에 AutoCAD Element들이 어떻게 저장되어 있는지 알아야만 하는 것 처럼..)

아래는 msElementDescr구조체의 구조와 샘플 이미지 입니다.

```c
struct msElementDescr                   /* defined in mselems.h*/
{
   struct
  {
    structMSElementDescr*next;        /* ptrto first entry in list */
    structMSElementDescr*previous;    /* ptrto last entry in list */
    structMSElementDescr*myHeader;    /* ptrto my hdr*/
    structMSElementDescr*firstElem;   /* ptrto first elemif header*/
    DgnModelRefP          *dgnModelRef; /* valid only if from cache */
    ElementRef            *elementRef;  /* valid only if from cache */
    Int32                 isHeader;     /* is this a complex header */
    Int32                 isValid;      /* INTERNAL USE ONLY */
    Int32                 userData1;    /* available for user */
    Int32                 userData2;    /* available for user */
  } h;
  MSElement el;                         /* elemdata */
};
```

- Sample element descriptors\
![](2011-07-05-32.jpg)