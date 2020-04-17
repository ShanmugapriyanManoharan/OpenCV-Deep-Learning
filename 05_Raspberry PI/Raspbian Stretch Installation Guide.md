# Raspberry Pi Installation Guide (Python and C++) for Single Core

Link to Download Raspbian Stretch: https://drive.google.com/file/d/1SgMxW5tDk-3YjUE8tFiUXgaDe5v_vygT/view?usp=sharing

# Step 1: Entering no sleep mode in your PC (Windows)
Recommended for Installation using Remote Access

a. Press the “Windows” key, type “Control Panel” to bring up the Apps page and then click “Control Panel” to open the window.

b. Click System and Security on the Control Panel window.

c. Click Power Options on System and Security window.

d. Click Choose when to turn off the display at the left side Options window.

e. Click all drop-down list to select Never for Turn off the display and Put the computer to sleep.

f. Click Save changes.

# Step 2: Expand filesystem

Type the following command to expand the Raspberry Pi3 file system:
'''
sudo raspi-config
'''

Then select the following:

Advanced Options > A1 Expand filesystem > Press Enter

# Step 3: Install Dependencies

a. The first step is to update and upgrade any existing packages:

'''shell
sudo apt-get update

sudo apt-get upgrade
'''

Then reboot your pi.

b. Install CMAKE developer packages:

'''shell
sudo apt-get install build-essential cmake pkg-config -y
'''
c. Install Image I/O packages:

sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev -y

d. Install Video I/O packages:

sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev -y

sudo apt-get install libxvidcore-dev libx264-dev -y

e. Install the GTK development library for basic GUI windows:

sudo apt-get install libgtk2.0-dev libgtk-3-dev -y

f. Install optimization packages (improved matrix operations for OpenCV):

sudo apt-get install libatlas-base-dev gfortran -y

# Step 4: Download the OpenCV 3.4 and contrib extra modules

cd

wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.4.0.zip

unzip opencv.zip

wget -O opencv\_contrib.zip https://github.com/Itseez/opencv\_contrib/archive/3.4.0.zip

unzip opencv\_contrib.zip

# Step 5: Compile and Install OpenCV 3.4.0 for Python and C++:

cd opencv-3.4.0

mkdir build

cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D BUILD_opencv_java=OFF \
-D BUILD_opencv_python2=ON \
-D BUILD_opencv_python3=ON \
-D PYTHON_DEFAULT_EXECUTABLE=$(which python3) \
-D INSTALL_C_EXAMPLES=ON \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D BUILD_EXAMPLES=ON\
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.0/modules \
-D WITH_CUDA=OFF \
-D BUILD_TESTS=OFF \
-D BUILD_PERF_TESTS= OFF ..

# Step 6: Swap Space size before compiling to add more virtual memory:

It will enable OpenCV to compile with all four cores of the Raspberry PI without any memory issues.
Open your /etc/dphys-swapfile and then edit the CONF\_SWAPSIZE variable


sudo nano /etc/dphys-swapfile

It will open the nano editor for editing the CONF\_SWAPSIZE. Change it like below:

\# set size to absolute value, leaving empty (default) then uses computed value

\# you most likely don't want this, unless you have an special disk situation

\# CONF\_SWAPSIZE=100 

CONF\_SWAPSIZE=1024 

Then save the changes you’ve made 

Then type the following lines to take it into effect

sudo /etc/init.d/dphys-swapfile stop

sudo /etc/init.d/dphys-swapfile start

# Step 7: Ready to be Compile:

Type the following command to compile it using  core of pi:

make clean

make

# Step 8: Install the build on Raspberry Pi:

After the successful build install the build using the following command: 

sudo make install 

sudo ldconfig

# Step 9: Verify the OpenCV build:

After running make install, OpenCV + Python bindings should be installed in
usr/local/lib/python3.5/dist-packages or usr/local/lib/python3.5/site-packages.

You need to use the site-packages or dist-packages. Look where it has been created and use
that site-packages or dist-packages. You can verify this with the ls command:


ls -l /usr/local/lib/python3.5/dist-packages/ 


Look for a name like cv2.so and if it is not there then look for a name like cv2.cpython-35m-
arm-linux-gnueabihf.so (name starting with cv2. and ending with .so). It might happen due
to some bugs in Python binding library for Python 3.


We need to rename cv2.cpython-35m-arm-linux-gnueabihf.so to cv2.so using the following
command:


cd /usr/local/lib/python3.5/dist-packages/


sudo mv /usr/local/lib/python3.5/dist-packages/cv2.cpython-35m-arm-linux-gnueabihf.so cv2.so

# Step 9: Don’t forget to change your swap size back!!!

Open your /etc/dphys-swapfile and then edit the CONF\_SWAPSIZE variable

sudo nano /etc/dphys-swapfile

It will open the nano editor for editing the CONF\_SWAPSIZE. Change it like below:

\# set size to absolute value, leaving empty (default) then uses computed value 

\# you most likely don't want this, unless you have an special disk situation 

CONF\_SWAPSIZE=100

\# CONF\_SWAPSIZE=1024


Then save the changes you’ve made

Then type the following lines to take it into effect

sudo /etc/init.d/dphys-swapfile stop

sudo /etc/init.d/dphys-swapfile start

# Step 10: Testing the Installation of Python and C++:

git clone https://github.com/sol-prog/raspberry-pi-opencv.git

cd raspberry-pi-opencv/tests

For testing Installation of C++:

g++ gui\_cpp\_test.cpp -o gui\_cpp\_test \`pkg-config --cflags --libs opencv\`

./gui\_cpp\_test


For testing Installation of Python:

python3 gui\_python\_test.py

# Installation has been completed

