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
  
