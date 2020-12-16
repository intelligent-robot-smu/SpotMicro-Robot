# SpotMicro-Robot [![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fpigzzz8815&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)

## SpotMicro-Robot's report.

## 개요

## 사용 도구 및 실행환경

raspberry pi 2B


## 소프트웨어 설치

1. pi image download
https://downloads.ubiquityrobotics.com/
ROS가 설치된 Ubuntu 16.04 기반의 pi image이다. 
링크에서 2020-02-10-ubiquity-xenial-lxde 버전 pi image를 다운로드 한다. 

**Window**

다운받은 파일은 xz형식의 zip파일이기 때문에 윈도우에서 해당 형식의 압축파일을 풀기 위해서는 7-zip을 통해서 해야한다. 
https://www.7-zip.org/ 에서 본인 Pc에 맞는 버전을 다운로드한다. 
다운로드 후 pi image 파일 우클릭해서 7-zip으로 압축을 푼다. 

<img width="352" alt="1" src="https://user-images.githubusercontent.com/18053479/101970256-ad815180-3c6c-11eb-979f-ad3d522c4a0e.PNG">

이렇게 img 파일이 생성된것을 이제 sd카드에 옮겨주어야한다. img파일을 sd카드에 옮겨주는 https://www.balena.io/etcher/ 를 다운로드한다.
실행하여 flash from file 에 img 파일을 넣고 select target에 sd카드를 선택해준 후 flash 한다. 

<img width="518" alt="2" src="https://user-images.githubusercontent.com/18053479/101970329-1b2d7d80-3c6d-11eb-8e08-081f2fcf5230.PNG">

이제 sd카드에 라즈베리파이와 ROS사용할 준비가 되었다.

2. 라즈베리파이 부팅

sd카드를 라즈베리파이에 삽입한다. 
모니터, HDMI, 마이크로 5핀, usb 마우스, 키보드 각각을 라즈베리파이 보드에 연결 후 부팅한다. 
ubuntu 초기 비밀번호 : ubuntu 로 접속한다. 

3. 원격 접속

4. swap memory

```sudo dphys-swapfile swapoff```

```sudo nano /etc/dphys-swapfile``` 와 같은 명령어로/etc/dphys-swapfile 파일에 들어가서 ```CONF_SWAPSIZE=1024``` 로 편집

```sudo dphys-swapfile setup```

```sudo dphys-swapfile swapon```

5. install catkin-tools

```$ sudo apt-get update```

```$ sudo apt-get install python-catkin-tools```

catkin-tools document : https://catkin-tools.readthedocs.io/en/latest/installing.html

catkin-ws 폴더에서 

```catkin_make -DCMAKE_BUILD_TYPE=Release```

## 서보 컨트롤

1. i2cpwm_board : ```rosrun i2cpwm_board i2cpwm_board``` 를 실행시킨다.

2. keyboard 활성화 : ```rosrun servo_move_keyboard servoMoveKeyboard.py```

3. 활성화키 명령 : 위의 코드로 










## 원문
[mike4192] - https://github.com/mike4192/spotMicro

###  프로젝트 참여자 : 이해선, 이성민

![SpotMicro-Robot's github stats](https://github-readme-stats.vercel.app/api?username=pigzzz8815&show_icons=true)

![SpotMicro-Robot's github stats](https://github-readme-stats.vercel.app/api?username=HaeSeon&show_icons=true)

[![solved.ac tier](http://mazassumnida.wtf/api/generate_badge?boj=intelligent-robot-smu)](https://solved.ac/intelligent-robot-smu)
