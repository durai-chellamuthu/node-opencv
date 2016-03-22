Node OpenCV for sercomm:
========================

git clone https://github.com/durai-chellamuthu/node-opencv.git

Making opencv for sercomm:
~~~~~~~~~~~~~~~~~~~~~~~~~~
cd node-opencv/opencv-2.4.11
mkdir build
cd build
cmake -DSOFTFP=OFF -DCMAKE_TOOLCHAIN_FILE=/media/d984c392-18b0-45fc-9e6f-180cb25d1e51/durai/projects/node-opencv-working-for-sercomm/checkin/node-opencv/opencv-2.4.11/platforms/linux/arm-gnueabi.toolchain.cmake ..
make -j2
make install

cd ../../

Making node-opencv for sercomm:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
export CC=/usr/local/linaro-multilib-2014.06-gcc4.9/bin/arm-linux-gnueabihf-gcc
export CXX=/usr/local/linaro-multilib-2014.06-gcc4.9/bin/arm-linux-gnueabihf-g++
export LD=/usr/local/linaro-multilib-2014.06-gcc4.9/bin/arm-linux-gnueabihf-g++
export AR=/usr/local/linaro-multilib-2014.06-gcc4.9/bin/arm-linux-gnueabihf-ar
export RANLIB=/usr/local/linaro-multilib-2014.06-gcc4.9/bin/arm-linux-gnueabihf-gcc-ranlib
export AS=/usr/local/linaro-multilib-2014.06-gcc4.9/bin/arm-linux-gnueabihf-as
export npm_config_arch=arm
export npm_config_nodedir=/media/d984c392-18b0-45fc-9e6f-180cb25d1e51/durai/tmp/node-v0.12.5-linux-armv7l
export GYP_CROSSCOMPILE=1
export GYP_DEFINES="OS=linux target_arch=arm arch=arm platform=linux arm_float_abi=hard node_abi=hard"
export OPENCV_DIR=/media/d984c392-18b0-45fc-9e6f-180cb25d1e51/durai/projects/node-opencv-working-for-sercomm/checkin/node-opencv/opencv-2.4.11/build
export PATH=$OPENCV_DIR/bin:$OPENCV_DIR/lib:$PATH
export PATH=/usr/local/linaro-multilib-2014.06-gcc4.9/bin/:$PATH
export PKG_CONFIG_PATH=/media/d984c392-18b0-45fc-9e6f-180cb25d1e51/durai/projects/node-opencv-working-for-sercomm/checkin/node-opencv/opencv-2.4.11/build/install/lib/pkgconfig/
npm install

cp -rf build/opencv/v5.0.0/Release/node-v14-linux-x64 build/opencv/v5.0.0/Release/node-v14-linux-arm

#Issue file command to confirm the opencv.node
file build/opencv/v5.0.0/Release/node-v46-linux-x64/opencv.node 
	build/opencv/v5.0.0/Release/node-v46-linux-x64/opencv.node: ELF 32-bit LSB shared object, ARM, version 1 (SYSV), dynamically linked, 		BuildID[sha1]=0xe3ce4d01952c7dc15cca4ca3b43aadd42b9a6aaf, not stripped



Commands to run in camera device terminal:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
telnet <device ip address>

##Enter username and password

mkdir durai
mount -t nfs -o nolock,proto=tcp,port=2049 10.0.0.27:/home/madhuram/madhu/durai/node-opencv /mnt/ramdisk/root/durai
mkdir durai_opencv
mount -t nfs -o nolock,proto=tcp,port=2049 10.0.0.27:/home/madhuram/madhu/durai/opencv-2.4.11 /mnt/ramdisk/root/durai_opencv
cd /mnt/ramdisk/root/durai_opencv/build/lib
export LD_LIBRARY_PATH=$PWD
cd /mnt/ramdisk/root/durai/examples

## Copy the node version 0.12.5 to the "/mnt/ramdisk/root/durai/examples" folder and issue following commands to test

./node-0.12.5 addweighted.js
./node-0.12.5 color-filter.js
./node-0.12.5 face-detection.js
./node-0.12.5 convert-image.js
./node-0.12.5 detect-shapes.js
./node-0.12.5 face-detection-rectangle.js
./node-0.12.5 quad-crosses.js
./node-0.12.5 remove-lines.js
./node-0.12.5 warp-image.js
