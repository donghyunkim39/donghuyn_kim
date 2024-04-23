# Ubuntu ROS1에서 USB_cam을 사용한 rostopic 출력

For the user who:  ubuntu에서 ROS1(Ros2x)을 사용자하는 사용자가 usb통신을 하는 Cam(ex. Webcam 등) package를 설치하고 usb_cam topic을 수신하는 과정을 진행한다.

Error 내용: 이전에 Ros1 사용자가 usb_cam package를 설치하고 catkin_make하면 ' Invoking "CMake" failed ' 오류가 뜬다.  
> => git clone으로 usb_cam package 다운시 Ros2 버전으로 다운받기 때문

## 1단계: usb_cam 패키지 설치



```bash
git init YOUR-REPOSITORY
```

