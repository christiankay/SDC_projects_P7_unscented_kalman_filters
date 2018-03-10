

# Unscented Kalman Filter Project

Self-Driving Car Engineer Nanodegree Program

Rubric [Here](https://review.udacity.com/#!/rubrics/783/view)



This project utilizes an Unscented Kalman Filter to estimate the state of a moving object of interest with noisy lidar and radar measurements. RMSE values are calculated to test the accuracy of the algorithm.  

This project involves the Term 2 Simulator which can be downloaded [here](https://github.com/udacity/self-driving-car-sim/releases)

This repository includes two files that can be used to set up and intall [uWebSocketIO](https://github.com/uWebSockets/uWebSockets) for either Linux or Mac systems. For windows you can use either Docker, VMware, or even [Windows 10 Bash on Ubuntu](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) to install uWebSocketIO. Please see [this concept in the classroom](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/16cf4a78-4fc7-49e1-8621-3450ca938b77) for the required version and installation scripts.

Once the install for uWebSocketIO is complete, the main program can be built and ran by doing the following from the project top directory.

1. mkdir build
2. cd build
3. cmake ..
4. make
5. ./UnscentedKF

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

---

### Important Dependencies
* cmake >= 3.5
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

### Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./UnscentedKF` Previous versions use i/o from text files.  The current state uses i/o
from the simulator.

---


### NIS (Normalized Innovation Squared)

One of the methods employed for testing accuracy and consistency was to use NIS (Normalized Innovation Squared). To calculate NIS, this method first measures the innovation, which is the difference between the estimated positions and the ground truth value. This difference is then normalized by the inverse of the vector S. NIS says that in a 3 dimentional space, approximately 5% of the NIS values should be over 7.8. with a proper implementation of your algorithm. This seems to hold about true when looking at the charts for lidar and radar NIS values:


![alt text][image1]


![alt text][image2]


### RMSE (Root Mean Square Error)

The minimum required RMSE values for this project are as follows: 

- X:  0.09

- Y:  0.10

- VX: 0.40

- VY: 0.30

The final values attained for this project were:

- X  0.0755

- Y  0.0845

- VX 0.3212

- VY 0.2494

### Improved Accuracy Of A New Algorithm

The RMSE values mentioned above can be compared to the old values I recieved from an extended kalman filter with the same radar and lidar measurements:

|  Old        |  New       | Accuracy Increase |
|:-----------:|:----------:|:-----------------:|
|X  0.0973   | X  0.0755  |  + 22  %          | 
|Y  0.0855   | Y  0.0845  |  + 1,1 %          | 
|VX  0.4512   | VX  0.3210 |  + 29  %          |
|VY  0.4399  | VY  0.2497 |  + 43  %          |

Overall a decent increase. My value for Y went down only a very small amount, but the other archived increases in accuracy, especially for velocity, clearly outweigh it. 

Reasons for accuracy increase:

The CRTV (Constant Turn Rate and Velocity Magnitude) model used for this project handles velocity much better than the model used for the extended kalman filter. This model is also better with non-linear functions.  


