# Ubuntu ROS1에서 USB_cam을 사용한 rostopic 출력

For the user who:  ubuntu에서 ROS1(Ros2x)을 사용자하는 사용자가 usb통신을 하는 Cam(ex. Webcam 등) package를 설치하고 usb_cam topic을 수신하는 과정을 진행한다.

1) Error 내용: 이전에 Ros1 사용자가 usb_cam package를 설치하고 catkin_make하면 ' Invoking "CMake" failed ' (CMakeLists.txt:69) 오류가 뜬다.  
> => git clone으로 기본 usb_cam package 다운시 Ros2 버전으로 다운받기 때문에 버전 불일치 문제.
![error1](https://github.com/donghyunkim39/donghuyn_kim/assets/163104650/a93404f4-a3e6-4f85-b414-9cc501f2dda0)


2) Error 내용: Ros1 버전으로 usb_cam package를 다운받았어도 ' No package 'libv4l2' found ' (CMakeLists.txt:10) 오류가 뜰때가 있다.
> => 이는 Error 내용에서 알수있듯이 'libv4l2' package가 없어서 생긴 오류이므로 package를 설치한다.
![error1](https://github.com/donghyunkim39/donghuyn_kim/assets/163104650/cb06191e-c9c0-4fac-86fb-e3c1cdbae020)


## 0단계(option): Package 다운받을 WS 폴더 만들기 

1) WS(폴더) 생성 #폴더 이름은 자유 but, 여기서 test_ws라고 함.
ubuntu 터미널창에 다음을 입력

```bash
mkdir -p ~/test_ws/src
```
2) catkin_make 진행
```bash
cd ~/test_ws/
```

```bash
catkin_make
```
3) 변경 설정 적용 (bash가 아닌 zsh 사용중이면 source devel/setup.zshrc
```bash
source devel/setup.bash
```



## 1단계: usb_cam 패키지 설치

1) 0단계에서 만든 폴더의 src폴더로 접속 (0단계 생략시 원하는 폴더의 src 폴더내로 접속)
새 터미널창을 열고
```bash
cd test_ws/src
``` 
 
1) ROS1(ROS) 버전 package 다운로드
```bash
git clone -b develop https://github.com/bosch-ros-pkg/usb_cam --recursive
```
git clone https://github.com/ros-drivers/usb_cam.git 로 package 다운로드시 오류가 떴던 이유는 이 주소로 package 다운받으면 ROS2 Branch가 default이기 때문이다.
따라서 ROS1을 지원하는 develop branch를 다운 받아준다.

2) catkin_make 진행
 ```bash
cd ~/test_ws/
```

```bash
catkin_make
```

여기까지 진행후 오류가 없다면 1단계의 4)로 jump 

만약 위에서 언급한 2) Error 내용 ' No package 'libv4l2' found ' (CMakeLists.txt:10) 가 발생한다면 아래 내용 계속 진행
![error1](https://github.com/donghyunkim39/donghuyn_kim/assets/163104650/ad542aa2-87bc-4d7b-860b-85bea6345b34)

3) package 'libv4l2' 다운

새 터미널창을 열고

```bash
sudo apt-get install -y libv4l-dev
```

4) 변경 설정 적용
test_ws 폴더 내에서 (src 폴더안이 아님) 빌드 적용 즉, cd ~/test_ws 상태에서
```bash
source devel/setup.bash
```

##2단계: usb_cam launch 파일 실행

1) roscore 실행
   
새 터미널창에서
```bash
roscore 
```

2) launch 파일 실행
```bash
roslaunch usb_cam usb_cam-test.launch
```
새 터미널창에서 
3) 
```bash
rostopic list 
```
입력하면 usb_cam 이 topic 으로 뜨는걸 확인할수있다.
캠확인은 터미널창에 rviz 혹은 rqt_image_view 로 확인 가능


