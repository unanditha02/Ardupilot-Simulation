# ardupilot-sim
Basic flight simulation using Ardupilot SITL


## Setting up ArduPilot for SITL

Instructions to set up ArduPilot environment on Ubuntu for Software-in-the-Loop simulations.

#### 1.  Update Ubunt/Linux and set up 'Git'
    sudo apt-get update
    sudo apt-get install git
    sudo apt-get install gitk git-gui
    

#### 2. Clone ardupilot repository
    git clone https://github.com/ArduPilot/ardupilot.
    cd ardupilot
    git submodule update --init --recursive

#### 3.  Install required packages
    cd Tools/environment_install
    ./install-prereqs-ubuntu.sh -y

#### 4.  Build with 'waf'
    ./waf configure --board CubeBlack
    ./waf copter


## Start SITL Simulator and TakeOff

    cd ardupilot/ArduCopter
    ../Tools/autotest/sim_vehicle.py -v ArduCopter --console --map

    mode guided
    arm throttle
    takeoff 40

## SITL with Gazebo

    Setup Gazebo interface [Instructions](https://ardupilot.org/dev/docs/using-gazebo-simulator-with-sitl.html#preconditions)

    gazebo --verbose worlds/iris_arducopter_runway.world
    ../Tools/autotest/sim_vehicle.py -f gazebo-iris --console --map


## Connecting with ROS

    roslaunch mavros apm.launch fcu_url:=udp://:14855@
