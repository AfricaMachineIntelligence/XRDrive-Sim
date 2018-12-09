# XRDrive-Sim
Platform | Build Status |
-------- | ------------ |
Anaconda | [![Build status](https://ci.appveyor.com/api/projects/status/swutsp1bjcc56q64/branch/master?svg=true)](https://ci.appveyor.com/project/ddiakopoulos/hand-tracking-samples/branch/master)

## Audience

The code in this repository is authored for computer-vision and machine-learning students and researchers interested in developing hand gesture applications using Intel® RealSense™ D400 depth cameras. The CNN implementation provided is intended to be used as a reference for training nets based on annotated ground-truth data; researchers may instead prefer to import captured datasets into other frameworks such as Google's TensorFlow and Caffe and optimize these algorithims using Model Optimizer from OpenVINO Toolkit.

This project provides Python code to demonstrate Hand Gestures via on PC camera or depth data, namely Intel® RealSense™ depth cameras. Additionally, this project showcases the utility of convolutional neural networks as a key component of real-time hand tracking pipelines using Intel OpenVINO. Two demo Jupyter Notebooks are provided showing hand gesture control from a webcam and depth camera.Vimeo demo-videos demonstrating some functionality of the XRDrive code can be found here: [XRDriveSim1-demo](https://vimeo.com/305377886) and [XRDriveSim2-demo](https://vimeo.com/305378325)

The software provided here works with the currently available Intel® RealSense™ D400 depth cameras supported by librealsense2. XRDrive is experimental code and not an official Intel® product.

## XRDrive Sim Notebooks and Python Samples

* [XRDrive_RealSense](xr_drive_realsense.ipynb) - This application demonstrates RealSense-based hand gesture to control keyboard and mouse while playing a racing game using DeepHandNet model

* [XRDrive_Cam](xr_drive_cam.ipynb) - This application demonstrates RealSense-based hand gesture to control keyboard and mouse while playing a racing game using DeepHandNet model

* [RealSense_Openpose](openpose.py) - This application demonstrates openpose.py using OpenVINO Toolkit and RealSense-based implementation of [opencv-dnn](https://github.com/opencv/opencv/blob/master/samples/dnn/openpose.py) re-implementaion from [Carnegie Mellon University OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose)

* [RealSense_resnet_ssd_face_python](resnet_ssd_face_python.py) - This application demonstrates resnet_ssd_face_python.py using OpenVINO Toolkit and RealSense-based implementation of [opencv-dnn](https://github.com/opencv/opencv/tree/master/samples/dnn)


# XRDrive Sim Hardware and Software

XRDrive is an inference-based application supercharged with power-efficient Intel® processors and Intel® Processor Graphics on a laptop.

1. ZenBook UX430
2. Intel Core i7 8th Gen
3. 16 GB DDR4 RAM
4. 512 SSD Storage
5. Intel RealSense D435
6. Ubuntu 18.04 LTS
7. ROS2OpenVINO
8. Anacodonda: Jupyter Notebook 
9. MxNet
10. Pyrealsense2
11. Pymouse

## Environment Setup
* Install ROS2 [Bouncy](https://github.com/ros2/ros2/wiki) ([guide](https://github.com/ros2/ros2/wiki/Linux-Development-Setup))<br>
* Install [OpenVINO™ Toolkit](https://software.intel.com/en-us/openvino-toolkit) ([guide](https://software.intel.com/en-us/articles/OpenVINO-Install-Linux))<br>
    	**Note**: Please use  *root privileges* to run the installer when installing the core components.
* Install OpenCL Driver for GPU
	```bash
	cd /opt/intel/computer_vision_sdk/install_dependencies
	sudo ./install_NEO_OCL_driver.sh
	```
* Install Intel® RealSense™ SDK 2.0 [(tag v2.14.1)](https://github.com/IntelRealSense/librealsense/tree/v2.14.1)<br>
	* [Install from source code](https://github.com/IntelRealSense/librealsense/blob/v2.14.1/doc/installation.md)(Recommended)<br>
	* [Install from package](https://github.com/IntelRealSense/librealsense/blob/v2.14.1/doc/distribution_linux.md)<br>

- Other Dependencies
	```bash
	# numpy
	pip3 install numpy
	# libboost
	sudo apt-get install -y --no-install-recommends libboost-all-dev
	cd /usr/lib/x86_64-linux-gnu
	sudo ln -s libboost_python-py35.so libboost_python3.so
	```


# 1. Research previous and current work on Hand Gestures

Xinghao Chen: awesome-hand-pose-estimation,
3DiVi: Nuitrack 3D Gestures,
Eyesight Embedded Computer Vision,
Carnegie Mellon University OpenPose: webcam,
Microsoft hololens: 3D sensor,
Microsoft hand tracking: 3D sensor,
Leap Motion: 3D sensor,
Mano Motion: smartphone camera,
PilotBit Mobile Hand Tracking: 3D sensor

# 2. Defining hand gestures to control keys on a keyboard and mouse.

Hand Gesture control keys for the keyboard are assigned to the left hand. Hand Gesture control keys for the mouse are assigned to the right hand. 
The normal has 10 key features:

1. closed hand
2. open hand
3. thumb only
4. additional index finger
5. additional middle finger
6. folding first finger
7. folding second finger
8. folding middle finger
9. folding index finger
10. folding thumb

We divided the left hand side into three regions (left, middle and right region). We use 3, 4, 5 as control, as a result we have 9 controls and 135 gestures that cover the keyboard. For a right hand as a mouse, all 10 features as gestures , which cover the inputs from mouse. The center of finger is a mouse cursor. The mouse cursor of computer will track the center of the right hand.

# 3. Data Collection

To train the DeepHandNet, big data is required and the data are to be collected by ourselves. We collected data from a variety of source including our own captured images, 2000 hand images were collected.




 
# 4. Training deep learning model which can recognize hand gestures at real time.
	## Training the MxNet DeepHandNet
Model is trained by 64x64 pixel images using Intel Architecture  
Data Preprocessing was done using OpenCV and Numpy to generate masked hand images. run xr_preprocessing_data.ipynb 
To recreate the Model run xrdrive_train_model.ipynb, It will read the preprocessed hand dataset, mask dataset and train the model, 400 epochs iterated.




