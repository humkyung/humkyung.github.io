---
title: "BsplineSurface에서 Mesh 데이타 구하기"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL, MSTN XM]
---

아래와 같은 단계를 통하여 BsplineSurface의 Mesh 데이타를 구할 수 있습니다.

1. MSElementDescr을 MSBsplineSurface 타입으로 변환
```cpp
MSBsplineSurface oBsplineSurf;
mdlBspline_convertToSurface(&oBsplineSurf , element);
```

2. BsplineSurface의 Mesh 데이타를 PolyfaceArray에 넣기
```cpp
PolyfaceArrays oPolyFaces;
memset(&oPolyFaces , 0x00 , sizeof(oPolyFaces));
oPolyFaces.pIndex = jmdlEmbeddedIntArray_grab();
oPolyFaces.pXYZ   = jmdlEmbeddedDPoint3dArray_grab();
oPolyFaces.pUV    = jmdlEmbeddedDPoint2dArray_grab();
if(SUCCESS == mdlMesh_polyfaceArraysFromMSBsplineSurface(&oPolyFaces , &oBsplineSurf , 1*mdlModelRef_getUorPerMaster(ACTIVEMODEL) , FALSE , TRUE))
{
    const int    nXYCount = jmdlEmbeddedDPoint3dArray_getCount(oPolyFaces.pXYZ ); 
    const int indexCount = jmdlEmbeddedIntArray_getCount(oPolyFaces.pIndex) ; 

    /// do something!!!
}
```

![BsplineSurface](2011-08-18-1.png)
_BsplineSurface_

![BsplineSurface의 Mesh 데이타](2011-08-18-2.png)
_BsplineSurface의 Mesh 데이타_

