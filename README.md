# SpotMicro-Robot [![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fpigzzz8815&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)

SpotMicro-Robot's report.


## What is Spot Micro Robot?  

open source robot으로 4족보행로봇이다. 앉기, 서기, 각도제어, 걷기를 할 수 있다. 



## 사용 도구 및 실행환경

* raspberry pi 2B
* ubuntu 16.04
* ROS 프레임워크
* C++
* Python


## 하드웨어 부품

3d 프린트 parts 뭐뭐 필요한지, 베터리, 서보 등 뭐뭐 필요한지 + 모델명


## 소프트웨어 설치


### 1. pi image download
https://downloads.ubiquityrobotics.com/
ROS가 설치된 Ubuntu 16.04 기반의 pi image이다. 

**_ROS?_**

개념 적기


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


### 2. 라즈베리파이 부팅

sd카드를 라즈베리파이에 삽입한다. 
모니터, HDMI, 마이크로 5핀, usb 마우스, 키보드 각각을 라즈베리파이 보드에 연결 후 부팅한다. 
ubuntu 초기 비밀번호 : ubuntu 로 접속한다. 

ROS가 포함된 파일을 받았기 때문에 뒤에 사용될 catkin_ws (catkin 작업 환경) 폴더가 있는것을 볼 수 있다. 


### 3. 원격 접속


### 4. swap memory

**_swap memory?_**

윈도우의 가상메모리와 같은 개념이다. ram 대신 disk영역을 쓰는 것 이다. 라즈베리파이 램이 부족하기 때문에 프로그램 실행시 메모리 초과가 있을 때를 대비해 swap을 통해 늘려준다. 라즈베리파이 3 이하 모델에서 사용할 경우 성능이 크게 좋아진다. 
but, 라즈베리파이의 sd카드 수명저하가 있을 수 있다.

부팅된 라즈베리파이에서 명령창을 켜고 다음 명령어를 입력한다. 


```sudo dphys-swapfile swapoff```   일시적으로 스왑을 중지한다. sudo로 명령어를 실행했기때문에 비밀번호를 입력해야한다. (ubuntu) 

```sudo nano /etc/dphys-swapfile```   와 같은 명령어로/etc/dphys-swapfile 파일에 들어가서 ```CONF_SWAPSIZE=1024``` 로 편집

```sudo dphys-swapfile setup```     스왑파일을 초기화한다. 

```sudo dphys-swapfile swapon```    스왑을 시작한다. 



### 5. install catkin-tools

**_catkin?_**
Catkin이란 rosbuild의 개선된 후속제품으로 ROS의 공식적인 Low level build system 이다. 

**_catkin-tools?_**
catkin 작업공간에서의 작업을 위한 명령어 도구를 제공하는 패키지이다. 
catkin 명령어로는 
+ build - catkin 작업공간에서 패키지를 빌드한다. 
+ config - catkin 작업공간의 레이아웃 및 설정을 구성한다. 
+ clean - catkin workspace에서 생성된 products를 지운다.
+ create - catkin package들의 구조를 생성한다. 
+ env - 수정된 환경에서 명령어를 실행한다. 
+ init - catkin workspace를 초기화한다. 
+ list - 작업공간 안에서의 catkin package들을 찾아서 리스트로 보여준다.

```$ catkin [global options] <verb> [verb arguments and options]``` 와 같은 형식으로 사용한다. 


명령창에서 다음과 같은 명령어를 입력한다. 

```$ sudo apt-get update```   운영체제에서 사용가능한 패키지들과 그 버전에 대한 정보를 업데이트한다. 즉 설치 가능한 리스트를 업데이트 한다. 

```$ sudo apt-get install python-catkin-tools``` catkin-tools를 설치한다. 

catkin-tools document : https://catkin-tools.readthedocs.io/en/latest/installing.html

catkin-tools를 사용하지 않고 ROS에 내장된 catkin_make를 사용할 경우 catkin-ws 폴더에서 다음 명령어를 사용한다. 

```catkin_make -DCMAKE_BUILD_TYPE=Release``` 


### 6. source code download

```git clone https://github.com/mike4192/spotMicro.git``` 

spot micro 오픈소스를 git에서 clone 하여 라즈베리파이에 다운로드한다. 다운로드 후 폴더 내부의 모든 파일을 catkin_ws/src 폴더에 넣어준다. 

    catkin_ws/
    │
    ├── src/
    │   ├── spot_micro_motion_cmd
    │   │   └── ...
    │   ├── spot_micro_keyboard_cmd
    │   │   └── ...  
    │   └── ...


즉 다음과 같은 폴더 하위구조가 생성되어있어야 한다. 
이제 해당 repository의 서브모듈을 받아주어야한다. 


**_git submodule?_**

서브모듈이란 git repository 아래에 다른 하위 git repository를 관리하기 위한 도구이다. 두 프로젝트를 서로 별개로 다루면서 그 중 하나의 프로젝트를 다른 프로젝트에 사용해야할 때 merge가 어려운 이슈를 해결하기 위해 git submodule을 사용한다.
```git submodule add [추가 저장소 URL]``` 와 같이 사용한다. 


그럼 이제 src 폴더 내에서 다음 명령어를 입력한다. 

    git submodule update --init --recursive
    git submodule update --recursive

submodule을 업데이트한다는 서브모듈의 변경사항을 업데이트한다는 뜻이다.
이 때 permission denied와 같은 권한오류가 나타난다면
.gitmodule 파일에 들어가서

        url = git@github.com:webhat/example.git

의 URL을 다음과 같이 변경한다. 

        url = https://github.com/webhat/example.git
    
그래도 안된다면 

.git/config
.git/modules/example/config 이 두 파일도 똑같이 바꿔준다. 그 후

    git submodule sync
    git submodule init
    git submodule update

를 명령창에 입력한다. 

이 에러는 git이 서버에서 repository를 다운도르할 때 공개키를 못찾아서 발생하는 것이다. 이 공개키를 찾기 위해 공개 URL로 바꿔주는 작업을 한 것이다. 

    

### 7. build

i2c 통신이란? GPIO를 제어하는데 쓰는 기술

GPIO : General Purposed IO. 일반적인 입출력을 제어할 수 있는 핀의 규약. 라즈베리파이에서 여러개의 핀들

즉 i2c를 활용하여 GPIO를 제어하기 위해서는 libi2c를 설치해야한다.  

```sudo apt-get install libi2c-dev``` 명령어를 통해 root폴더에서 libi2c를 설치한다. 


```catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release``` catkin 작업공간의 구성을 다음과 같이 설정한다. 

```catkin build``` 프로젝트를 빌드한다.

빌드시 이미 build 폴더가 있다는 에러메세지가 나오면 작업공간을 clean 해준다. 

build가 완료되면 다음과 같은 화면이 뜬다. 

<img width="500" alt="로그인창" src="https://user-images.githubusercontent.com/18053479/102469198-cedfa480-4095-11eb-9fbe-fae8a6fd9da0.jpg">




## 서보 컨트롤

### 라즈베리파이와 서보모터 연결

우선 예시로 1개의 서보를 실행시켜본다. 

**_PWN?_**

Pulse Width Modulation으로 펄스의 폭을 조절하여 주기를 제어하는 방법이다. 펄스가 0이 아닐 때 전기가 흘러 작동하는것이다. 펄스의 유지시간이 길면 계속 작동하고 펄스가 짧다면 유지시간이 짧아진다. 


다음 표와 같이 라즈베리파이 보드와 서보모터를 연결한다. 
GPIO : General Purposed IO. 일반적인 입출력을 제어할 수 있는 핀의 규약 

|Pi GPOI pin|PCA9685|
|---|---|
|1|VCC|
|2|V+|
|3|SDA|
|5|SCL|
|6|GND|

```sudo i2cdetect -y 1```를 통해 i2c 연결된 위치를 확인한다. 즉 PWM 컨트롤러의 i2c가 어느 채널에 연결되어있는지

연결을 확인하였으면 서보모터를 제어해볼 파일을 다운받는다. 

    git clone https://github.com/adafruit/Adafruit_Python_PCA9685.git
    cd Adafruit_Python_PCA9685
    sudo python setup.py install

다운받은 위치로 이동한 후 

```sudo python gpio_pwm_servo_motor.py```를 실행하면 서보모터가 움직인다. 


<img width="700" alt="servo" src="https://user-images.githubusercontent.com/18053479/102475764-a0fe5e00-409d-11eb-88c9-fc87e2aa0e59.gif">



### 서보 연결 구성도


### 서보 컨트롤 설명

1. i2cpwm_board : ```rosrun i2cpwm_board i2cpwm_board``` 를 실행시킨다.

2. keyboard 활성화 : ```rosrun servo_move_keyboard servoMoveKeyboard.py```

3. 활성화키 명령 :  

<img width="518" alt="3" src="https://user-images.githubusercontent.com/58153959/102410776-60b6c580-4034-11eb-84e8-18272cf93609.png" width="90%"></img>


## 조립



## 로봇 4족보행 시키기 

보행 메커니즘 설명



## 원문
[mike4192] - https://github.com/mike4192/spotMicro


###  프로젝트 참여자 : 이해선, 이성민

![SpotMicro-Robot's github stats](https://github-readme-stats.vercel.app/api?username=pigzzz8815&show_icons=true)

![SpotMicro-Robot's github stats](https://github-readme-stats.vercel.app/api?username=HaeSeon&show_icons=true)

[![solved.ac tier](http://mazassumnida.wtf/api/generate_badge?boj=intelligent-robot-smu)](https://solved.ac/intelligent-robot-smu)
