---
title: "VB를 통한 FrameWork 자동 로드"
comments: true 
img_path: /assets/images/USTN/
categories: [USTN]
tags: [MDL]
---

FrameWork을 자동으로 로딩하는 것에 대해 알아봅시다. 물론 PC에 FrameWork이 설치되어 있어야 하겠지요.

1. 현재 디렉토리를 Microstation이 설치되어 있는 디렉토리로 설정합니다.(SetCurrentDirectory)
2. Shell을 이용해서 mod 폴더에 있는 FrameWork dgn 파일을 오픈합니다.
3. Set msApp = GetObject("" , "Microstation.Application")
4. fwstart.ma 파일을 로드합니다.
> msApp.MbeSendCommand("MDL LOAD FWSTART.MA")\
> 다시 시간이 걸립니다.

이렇게 하면 성공적으로 FRAMEWORK을 로드할수 있습니다.

한가지 주의할 사항은 위의 절차대로 하기 전에 반드시 MS , FW_PRODUCT 이 두 환경변수를 설정해 줘야 한다는 겁니다.\
예)\
```sh
"FW_PRODUCT"="C:\\WIN32APP\\INGR\\FWPLUS\\"
"MS"="C:\\Bentley\\Program\\MicroStation\\ustation.exe"
```