---
title: "Synology NAS에 AirVideo 서버 설치하기"
comments: true 
categories: [Synology]
tags: [Sonology, NAS, AirVideo]
---

Air Video Server 를 설치하기 전에 먼저 Bootstrap을 설치해 주셔야 합니다.\
이에 대한 내용은 생략 ...

자세한 설명은 제일 아래 참고 사이트에 들어가시면 보실 수 있습니다.\
댓글도 읽어보시면 많은 도움이 됩니다.

지금부터 시작하겠습니다.

--------

제가 작업한 환경 그대로 적겠습니다.\
작업 디렉토리는 임의로 바꾸셔도 됩니다.

1. 설치 환경\
접속 방법 : ssh\
유저 : root\
작업디렉토리 : /opt/etc\
Air Video Server 설치 디렉토리 : /opt/air_video\
Java 설치 디렉토리 /opt/java\
\
/etc/profile에 아래 내용을 추가하거나 수정합니다.\
수정 후에는 로그오프하고 로그온 하시거나  .(점) /etc/profile 명령어를 실행합니다.\
```sh
PATH=/usr/bin:/bin:/usr/sbin:/sbin:/usr/syno/bin:/usr/syno/sbin:/opt/bin:/opt/sbin:/opt/java/bin:/opt/arm-none-linux-gnueabi/bin
LD_LIBRARY_PATH=/opt/lib:/lib:/opt/arm-none-linux-gnueabi/lib
LD_RUN_PATH=/opt/lib:/lib:/opt/arm-none-linux-gnueabi/lib
JAVA_HOME=/opt/java
export PATH LD_LIBRARY_PATH LD_RUN_PATH JAVA_HOME
LANG="ko_KR.UTF-8"
LC_ALL="ko_KR.UTF-8"
SUPPORTED="ko_KR.UTF-8:ko_KR:ko"
export LANG LC_ALL SUPPORTED
```

2. 패키지 설치
다행히도 대부분은 패키지 형태로 설치가 가능합니다.\
\
```
ipkg install optware-devel
ipkg install gcc
ipkg install git
ipkg install grep
ipkg install sdl
ipkg install sdl-dev
ipkg install libmpeg2
ipkg install mpeg2dec
ipkg install libpth
ipkg install lame
ipkg install faad2
ipkg install xvid
ipkg install jpeg
ipkg install vim
```
여기까지는 아주 쉽게 설치가 진행됩니다.

3. faac 설치\
```sh
wget http://switch.dl.sourceforge.net/sourceforge/faac/faac-1.28.tar.gz
tar -xzf faac-1.28.tar.gz
cd faac-1.28
./configure --prefix=/opt --without-mp4v2
make
make install
```
이것도 별 문제없이 설치가 됩니다.

4. x264 설치\
ipkg의 패키지가 구버전이라서 최신 버전으로 다운받아 설치해야 합니다.\
\
패키지가 업데이트되면 이 과정이 1번으로 이동하겠군요.\
```sh
git clone git://git.videolan.org/x264.git
cd /opt/etc/x264
./configure --prefix=/opt --disable-asm
make
make install
```

5. Library 링크 설정
```sh
cd /opt/lib
ln -s libxvidcore.so.4.2 libxvidcore.so
ln -s libxvidcore.so.4.2 libxvidcore.so.4
ln -s libx264.so.106 libx264.so
```
\
일부 라이브러리의 링크가 제대로 안되어 있어 링크를 설정해 줍니다.

6. mp4creator 설치\
이것 때문에 무지 많이 고생을 했습니다.\
완벽한 컴파일이 안되고 에러가 납니다만 필요한 파일은 얻을 수 있습니다.\
\
http://sourceforge.net/projects/mpeg4ip/ 접속하여 소스 다운\
==> 이것은 wget으로 받아지지 않더군요.
```sh
tar -xzf mpeg4ip-1.5.0.1.tar.gz
cd mpeg4ip-1.5.0.1
```
\
소스코드를 조금 손봐야 하는데 vi에디터 기준으로 설명합니다.\
적당한 에디터로 아래와 같이 수정하시면 됩니다.\
```sh
vim +1733 lib/rtp/rtp.c
```
\
i를 누르고 아래와 같이 세 줄 앞에 // 로 주석처리해줍니다.\
```c
//if (((packet->common.count * 6) + 1) < (ntohs(packet->common.length) - 5)) {
//  rtp_message(LOG_NOTICE, "Profile specific SR extension ignored");
//}
```  
\
ESC키를 누르고 :wq 엔터 눌러 저장하고 종료합니다.
\
```sh
vim +1752 lib/rtp/rtp.c
```
여기도 마찬가지로 i를 누르고 세 줄 앞에 // 로 주석처리해 줍니다.
```c 
//if (((packet->common.count * 6) + 1) < ntohs(packet->common.length)) {
//  rtp_message(LOG_INFO, "Profile specific RR extension ignored");
//}
```
ESC키를 누르고 :wq 엔터 눌러 저장하고 종료합니다.\
./bootstrap --prefix=/opt --disable-mp4live --disable-mp4live-alsa\
make ERROR # 발생하지만 무시합니다.\
\
cd lib\
make install # ERROR 발생하지만 무시합니다.\
\
cd ../server\
make install

7. ffmpeg-for-2.2.5 설치\
wget http://www.inmethod.com/air-video/download/ffmpeg-for-2.2.5.tar.bz2\
tar jxf ffmpeg-for-2.2.5.tar.bz2\
\
./configure --prefix=/opt --enable-static --disable-shared --enable-gpl \
--enable-nonfree --enable-libfaac --enable-libfaad --enable-libfaadbin \
--enable-libmp3lame --enable-libx264 --enable-libxvid --disable-asm \
--disable-decoder=aac
\
make\
make install

8. Java 설치\
ARMv5용 Java SE를 다운받아 설치해야 합니다.\
다운받기 위해서는 몇 가지 정보를 입력해야 합니다. (이름, 이메일주소 등)\
\
Java SE for Embedded evaluation downloads page: 
http://java.sun.com/javase/downloads/embedded.jsp
\
아래 파일을 다운받으시면 됩니다.
ejre-1_6_0_10-fcs-b42-linux-armv5-sflt-eabi-headless-10_jun_2010.tar.gz
```sh
cd /opt
tar xfz ejre-1_6_0_10-fcs-b42-linux-armv5-sflt-eabi-headless-10_jun_2010.tar.gz
ln -s ejre1.6.0_10 java
```

9. Air Video Server 설치
```sh
md /opt/air_video
cd /opt/air_video
```
\
아래 URL에 접속하시면 최신의 파일을 다운받으실 수 있습니다.\
\
http://inmethod.com/forum/posts/list/1856.page\
\
지금 현재(2010-10-09) 가장 최신의 리눅스용 파일의 버전은 alpha4 입니다.\
```sh
wget http://inmethod.com/air-video/download/linux/alpha4/AirVideoServerLinux.jar
```

10. Air Video 설정파일 만들기\
vi /opt/air_video/test.properties\
\
path.ffmpeg = /opt/bin/ffmpeg\
path.faac = /opt/bin/faac\
path.mp4creator = /opt/bin/mp4creator\
password =\
subtitles.encoding = UTF-8\
subtitles.font = Verdana\
folders = Movie:/volume1/movie,Video:/volume1/video (제목:경로,제목:경로,...)

11. Air Video Server 구동하기
```sh
/opt/java/bin/java -jar /opt/air_video/AirVideoServerLinux.jar /opt/air_video/test.properties
```
\
-jar 빼먹지 마세요.

11. 참고 자료
* 우분투에서 에어비디오 서버 구동하기\
http://clien.career.co.kr/cs2/bbs/board.php?bo_table=lecture&wr_id=64177&page=0
* Video-Streaming from QNAP NAS via AirVideo to iPad or iPhone\
http://forum.qnap.com/viewtopic.php?f=177&t=32731
* AirVideo Server under Linux\
http://wiki.birth-online.de/know-how/hardware/apple-iphone/airvideo-server-linux

출처 : DS210j에 Air Video Server 설치하기 (시놀로지 NAS) |작성자 저스틴