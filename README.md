# bebop_xbox_joystick
Control the Bebop Drone using the xbox joystick

**A good tip is to always have ROS running in the background whenever you work.**

    

**Make a new catkin workspace:**

    mkdir -p ~/catkin_ws_bebop/
  
    catkin_make
  
    cd src

**Download parrot wrapper:**

    git clone https://github.com/antonellabarisic/parrot_arsdk.git
    
    cd parrot_arsdk
    
    git checkout noetic_dev
    
    sudo apt-get install libavahi-client-dev
    
    sudo ln -s /usr/bin/python3
    
    cd ~/catkin_ws_bebop/
    
    catkin_make
  
**Download the bebop autonomy package:**

    cd ~/catkin_ws_bebop/src
    
    git clone https://github.com/autonomylab/bebop_autonomy.git
    
    cd bebop_autonomy
    
    cd bebop_driver
    
    cd src
  
  **Open bebop video decoder file:**
  
    gedit bebop_video_decoder.cpp
  
  **We will have to make some changes**
  
  **Modify:**
  
   **in line 93: replace CODEC_CAP_TRUNCATED with AV_CODEC_CAP_TRUNCATED**
  
   **in line 95: replace CODEC_FLAG_TRUNCATED  with  AV_CODEC_FLAG_TRUNCATED**
            
   **in line 97: replace CODEC_FLAG2_CHUNKS  with  AV_CODEC_FLAG2_CHUNKS**
   
   
   **Add this line in your ~/.bashrc:** 
   
   
      export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:<path_to_your_catkin_ws>/devel/lib/parrot_arsdk
   
   
   **Install joystick teleoperation packages:**
   
      cd ~/catkin_ws_bebop/
      
      sudo apt install ros-noetic-joy ros-noetic-joy-teleop ros-noetic-teleop-twist-joy
      
      cd ~/catkin_ws_bebop/
      
      catkin_make
     
   **If an error is produced after building the workspace with "catkin_make", running it again will solve it**
   
   **Since we are running with the catkin workspace, we must source it:**
   
        source ~/catkin_ws_bebop/devel/setup.bash
        
   **We will be running our program as a nodelet to have access to the on board camera**
   
   **Run the nodelet manager:**
            
      rosrun nodelet nodelet manager_name:=nodelet_manager
      
   **Turn on the drone from the battery pack. Make sure that there are no blades installed on the drone.**
   
   **Connect to the Bebop's Wifi: BebopDrone-B051013**
   
   **Establish a connection with the drone:**
   
        cd catkin_ws_bebop
        
        roslaunch bebop_tools bebop_nodelet_iv.launch 
        
   **You will now see a video feed of the drone appear on your screen, open a new window, then source it:**
   
        source /opt/ros/noetic/setup.bash
        
   **You can now tell the drone to takeoff:**
   
        rostopic pub --once bebop/takeoff std_msgs/Empty
        
   **The drone can be landed:**
   
        rostopic pub --once bebop/land std_msgs/Empty
        
   **We are now ready to start operating the drone with the controller**

   **There is the option to operate the drone with the joystick, but this will cover use of the Xbox 360 controller**
   
   **Connect your controller and review the numbers assigned to the buttons using:**
        
        sudo jstest /dev/input/js0 
        
   **Your screen should look like this:**
   ![Screenshot from 2022-04-12 16-55-57](https://user-images.githubusercontent.com/103221005/163067891-cb53de4f-c312-4d28-8e78-56a5b416456b.png)

        
   **We will navigate to the xbox360.yaml file. This file includes the mapping of buttons, and the actions the drone will do**
   
        cd ~/catkin_ws_bebop/src
        
        cd bebop_autonomy
        
        cd bebop_tools
        
        cd config
        
        gedit xbox360.yaml
        
  **Please take notes on these commands, and have them handy for when you use the drone. Pay attention to the "deadman" buttons. The deadman button acts like a safety switch. The deadman buttons correlate to the buttons on the controller. You will not be able to make the drone flip, for example, without having their deadman buttons engaged. NOTE:RB must be engaged to pilot**
        
 **It is now time to teleoperate the Bebop**
 
 **Source the catkin:**
 
        source ~/catkin_ws_bebop/devel/setup.bash
        
  **Run the nodelet manager:**
  
        rosrun nodelet nodelet manager_name:=nodelet_manager
        
        cd ~/catkin_ws_bebop/src
        
  **Turn the drone on, and connect to its wifi. Run the nodelet:**
  
        roslaunch bebop_tools bebop_nodelet_iv.launch
        
  **Open a new tab. You will now have access to the drone's video footage.**
  **We are allowed to source the Bash due to the changes made to it from earlier:**
  
        source ~/.bashrc
            
  **Navigate to the joy-teleop launch file and launch it:**
  
        cd ~/catkin_ws_bebop/src/bebop_autonomy/bebop_tools/launch
        
        roslaunch joy_teleop.launch
        
   **The controller is now connected to the drone, open a new tab and open the controller test for reference:**
    
          sudo jstest /dev/input/js0 
          
   **You are now ready to pilot the drone!**
  
        
