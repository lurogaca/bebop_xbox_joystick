# bebop_xbox_joystick
Control the Bebop Drone using the xbox joystick


**Make a new catkin workspace**

    mkdir -p ~/catkin_ws_bebop/
  
    catkin_make
  
    cd src

**Download Parrot Wrapper**

    git clone https://github.com/antonellabarisic/parrot_arsdk.git
  
    cd parrot_arsdk
  
    git checkout noetic_dev
  
    sudo apt-get install libavahi-client-dev
  
    sudo ln -s /usr/bin/python3
  
    cd ~/catkin_ws_bebop/
  
    catkin_make
  
**Downloading Bebop Autonomy**

     cd ~/catkin_ws_bebop/src
  
    git clone https://github.com/autonomylab/bebop_autonomy.git
  
    cd bebop_autonomy
  
     cd bebop_driver
  
     cd src
  
  **Open Bebop Video Decoder File**
  
    gedit bebop_video_decoder.cpp
  
  **We will have to make some changes**
  
  **Modify: line 93: CODEC_CAP_TRUNCATED   into   AV_CODEC_CAP_TRUNCATED**
  
   **line 95: CODEC_FLAG_TRUNCATED   into    AV_CODEC_FLAG_TRUNCATED**
            
   **line 97: CODEC_FLAG2_CHUNKS   into   AV_CODEC_FLAG2_CHUNKS**
   
   
   **Install Joystick Teleoperation Packages**
   
      cd ~/catkin_ws_bebop/
      
      sudo apt install ros-noetic-joy ros-noetic-joy-teleop ros-noetic-teleop-twist-joy
      
      cd ~/catkin_ws_bebop/
      
      catkin_make
   
   **Since we are running with the catkin workspace, we must source it**
   
        source ~/catkin_ws_bebop/devel/setup.bash
        
   **We will be running our program as a nodelet to have access to the on board camera**
            
      rosrun nodelet nodelet manager_name:=nodelet_manager
