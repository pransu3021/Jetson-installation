# Jetson-installation

Steps to install and Setup Jetson Nano.
By Flashing SDK
Download BalenoEtcher from the below link.
https://www.balena.io/etcher/
Click on the below link and download the Jetson Nano Developer Kit SD Card Image from the step 1.
https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write
Use Etcher to write the Jetson Nano Developer Kit SD Card Image to your microSD card
•	Launch Etcher and Click “Select image” and choose the zipped image file downloaded earlier.
•	Insert your microSD card if not already inserted
•	Click “Select drive” and choose the correct device.
•	Click “Flash!”
After Flashing the SD Card, setup the Jetson Nano and Start the PC and just follow the instruction as follows.
Time zone- select India, password for Shashank set “s”  and on next slide instead of numbers put 0 and click next.
Open Terminal
1.	Install system packages required by TensorFlow:
$ sudo apt-get update
$ sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran
2.	Install and upgrade pip3.
$ sudo apt-get install python3-pip
$ sudo pip3 install -U pip testresources setuptools==49.6.0  
$ sudo pip3 install -U numpy==1.19.4 future==0.18.2 mock==3.0.5 h5py==2.10.0 keras_preprocessing==1.1.1 keras_applications==1.0.8 gast==0.2.2 futures protobuf pybind11

3.	Click on the below link and clone the github library 
https://github.com/rbonghi/jetson_stats
4.	Extract the zip file and open the terminal from the extracted folder and install the Jetson-Stats using below command
sudo -H pip3 install -U jetson-stats

After installing jtop reboot the system.
5.	Install the Python package dependencies.
sudo pip3 install -U numpy future mock h5py gast futures protobuf pybind11
6.	Installing Tensorflow. (Check Tensorflow release note for proper version.)
sudo pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44  tensorflow==1.15.3+nv20.09
7.	Click on the below link and download the .deb file of DeepStream 5.0.1 for Jetson
https://developer.nvidia.com/deepstream-getting-started
8.	Click on the below link and follow the steps in Quic k start guide Or follow the below setups.
https://docs.nvidia.com/metropolis/deepstream/5.0/dev-guide/index.html#page/DeepStream_Development_Guide/deepstream_quick_start.html#
 To install additional packages
•Enter the following commands to install the prerequisite packages:
$ sudo apt install \
libssl1.0.0 \
libgstreamer1.0-0 \
gstreamer1.0-tools \
gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad \
gstreamer1.0-plugins-ugly \
gstreamer1.0-libav \
libgstrtspserver-1.0-0 \
libjansson4=2.11-1

To install librdkafka (to enable Kafka protocol adaptor for message broker)
1.Clone the librdkafka repository from GitHub: (in Downloads folder)
$ git clone https://github.com/edenhill/librdkafka.git
2.Configure and build the library:
$ cd librdkafka
$ git reset --hard 7101c2310341ab3f4675fc565f64f0967e135a6a
./configure
$ make
$ sudo make install

3.Copy the generated libraries to the deepstream directory:
$ sudo mkdir -p /opt/nvidia/deepstream/deepstream-5.0/lib 
$ sudo cp /usr/local/lib/librdkafka* /opt/nvidia/deepstream/deepstream-5.0/lib

To install latest NVIDIA V4L2 GStreamer plugin
4. Open the apt source configuration file in a text editor, for example:
$ sudo vi /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
5. Change the repository name and download URL in the deb commands shown below:
deb https://repo.download.nvidia.com/jetson/common r32.4 main
deb https://repo.download.nvidia.com/jetson/<platform> r32.4 main
Where <platform> identifies the platform’s processor:
•t186 for Jetson TX2 series
•t194 for Jetson AGX Xavier series or Jetson Xavier NX
•t210 for Jetson Nano or Jetson TX1
For example, if your platform is Jetson Xavier NX:
•deb https://repo.download.nvidia.com/jetson/common r32.4 main
•deb https://repo.download.nvidia.com/jetson/t194 r32.4 main
6. Save and close the source configuration file.
7. Enter the commands:
$ sudo apt update
$ sudo apt install --reinstall nvidia-l4t-gstreamer

To install the DeepStream SDK Using the DeepStream Debian package

Put the file name for Deepstream 5.0.1 which is downloaded in above step no.7.in the below command where the folder is saved:
$ sudo apt-get install ./deepstream-5.0_5.0.0-1_arm64.deb

Python Bindings

Click the below link and download the Github File and Extract the downloaded file.

https://github.com/NVIDIA-AI-IOT/deepstream_python_apps

Open the Extracted folder and open HOWTO.md file and follow the instructions as follows in the downloads terminal.

$ sudo apt-get install python-gi-dev
$ export GST_LIBS="-lgstreamer-1.0 -lgobject-2.0 -lglib-2.0"
$ export GST_CFLAGS="-pthread -I/usr/include/gstreamer-1.0 -I/usr/include/glib-2.0 -I/usr/lib/x86_64-linux-gnu/glib-2.0/include"
$ git clone https://github.com/GStreamer/gst-python.git
$ cd gst-python
$ git checkout 1a8f48a
$ ./autogen.sh PYTHON=python3
$ ./configure PYTHON=python3
$ make
$ sudo make install

Rename the deepstream_python_apps-master as deepstream_python_apps.


$ sudo cp –r $path of deepstream_python_apps to $destination folder path

Destination folder path as follows:

Click on Other Locations/Computer/
opt/nvidia/deepstream/deepstream-5.0/sources

Go the below destination and open readme and follow the steps

Sources/deepstream_python_apps/apps/deepstream-test3/

To run sample videos run below command:

Python3 deepstream_test_3.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/sample_1080p_h265.mp4

