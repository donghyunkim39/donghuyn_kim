# Ubuntu ROS1에서 USB_cam을 사용한 rostopic 출력

For the user who:  ubuntu에서 ROS1(Ros2x)을 사용자하는 사용자가 usb통신을 하는 Cam(ex. Webcam 등) package를 설치하고 usb_cam topic을 수신하는 과정을 진행한다.

1) Error 내용: 이전에 Ros1 사용자가 usb_cam package를 설치하고 catkin_make하면 ' Invoking "CMake" failed ' (CMakeLists.txt:69) 오류가 뜬다.  
> => git clone으로 기본 usb_cam package 다운시 Ros2 버전으로 다운받기 때문에 버전 불일치 문제.
![error1](https://github.com/donghyunkim39/donghuyn_kim/assets/163104650/a93404f4-a3e6-4f85-b414-9cc501f2dda0)


2) Error 내용: Ros1 버전으로 usb_cam package를 다운받았어도 ' No package 'libv4l2' found ' (CMakeLists.txt:10) 오류가 뜰때가 있다.
> => 이는 Error 내용에서 알수있듯이 'libv4l2' package가 없어서 생긴 오류이므로 package를 설치한다.

## 1단계(option): Package 다운받을 WS 폴더 만들기 

#1) WS(폴더) 생성 #폴더 이름은 자유 but, 여기서 test_ws라고 함.
ubuntu 명령창에 다음을 입력

```bash
mkdir -p ~/test_ws/src
```
#2) catkin_make 진행
```bash
cd ~/test_ws/
```

```bash
catkin_make
```

```bash
source devel/setup.bash
```


## 2단계: usb_cam 패키지 설치



```bash
git clone -b develop https://github.com/bosch-ros-pkg/usb_cam --recursive
```
git clone https://github.com/ros-drivers/usb_cam.git 로 package 다운로드시 오류가 떳던 이유는 이주소로 package 다운받으면 ROS2 Branch가 default이기 때문이다.
따라서 ROS1을 지원하는 develop branch를 다운 받아준다.
