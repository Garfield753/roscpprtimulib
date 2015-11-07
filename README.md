# roscpprtimulib - C++ app demonstrating RTIMULib with ROS
This is a C++ demo program showing how RTIMULib can be used with ROS. It is essentially the same as Romain Reignier's original implementation (https://github.com/romainreignier/rtimulib_ros) with a few small tweaks. In particular, the publish rate is now the same as the sample rate and accelerations are sent in m/s/s.

The contents of this repo are released under the the BSD license.

## Build
Testing was performed using ROS Jade on a Raspberry Pi 2 running Ubuntu 14.04. ROS Jade should be installed from here - http://wiki.ros.org/jade/Installation/UbuntuARM.

### Installing RTIMULib
The first thing to do is to clone the RTIMULIb repo:

        cd ~
        git clone git://github.com/richards-tech/RTIMULib
        
Alternatively clone RTIMULib2 instead of RTIMULib to get the latest developments including simplified magnetometer calibration.

To use roscpprtimulib it is necessary to install RTIMULib using the CMake method:

        cd RTIMULib/Linux
        mkdir build
        cd build
        cmake .. -DBUILD_DEMO=0 -DBUILD_GL=0
        make -j4
        sudo make install
        sudo ldconfig

### ROS build
Once the appropriate RTIMULib install has been performed enter:

        cd ~/
        git clone git://github.com/richards-tech/roscpprtimulib
        cd roscpprtimulib 
        catkin_make
        source devel/setup.sh
    
## Run
If roscore is running on a different machine, add the following two lines to the .bashrc file on the Raspberry Pi 2:

        export ROS_MASTER_URI=http://<roscore IP address>:11311
        export ROS_IP=<raspberry pi IP address>

To run roscpprtimulib enter:

        roslaunch roscpprtimulib roscpprtimulib.launch
    
rostopic can be used to check if things are working:

        rostopic echo /imu

## Calibration
As usual, magnetometer calibration is an issue and calibration needs to be performed using the RTIMULibCal program in the RTIMULib repo - https://github.com/richards-tech/RTIMULib/tree/master/Linux/RTIMULibCal. The resulting RTIMULIb.ini should be copied into the package directory.

