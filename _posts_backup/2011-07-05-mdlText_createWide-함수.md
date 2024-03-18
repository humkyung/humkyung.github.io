---
title: "mdlText_createWide 함수"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN J]
---

mdlText_create대신 mdlText_createWide를 사용하는 가장 큰 이유는 텍스트의 기울기를 줄수 있기 때문이다.

```c
int mdlText_createWide
(
    MSElementUnion *out, /* <= text element created */
    MSElementUnion *in, /* => template element */
    MSWideChar *wString, /* => wide character string */
    Dpoint3d *userOrigin, /* => origin (or NULL) */
    RotMatrix *rMatrix, /* => rotation matrix (or NULL) */
    TextSizeParam *textSize, /* => size (or NULL) */
    TextParamWide *txtParamWide, /* => parameters (or NULL) */
    TextEDParam *edParam /* => enter data info (or NULL) */
);
```

mbstowcs 함수를 통하여 char*를  MSWideChar*로 변환시킬 수 있습니다.

여기서 한가지 주의해야 할 것은 txtParamWide의 flag들의 속성을 제대로 설정해주어야 한다는 것이다.\
예를 들어 txtParamWide.flags.vertical을 FALSE로 하지 않으면 텍스트들이 Vertical 방향으로 쓰여지게 된다.

txtParamWide.flags.vertical을 FALSE로 두고 텍스트의 회전은 rMatrix에서 설정을 하면 된다.

이번 프로젝트에서 이 문제로 인해 며칠동안 고민을 했었습니다.