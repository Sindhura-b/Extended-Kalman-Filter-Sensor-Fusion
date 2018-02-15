# Sensor Fusion and Object Tracking using Extended Kalman Filter

In this project extended kalman filter has been utilized to estimate the state of a moving object of interest with noisy lidar and radar measurements. The developed algorithm is tested on two different different datasets provided in the Udacity's Simulator and experimented till the RMSE values that determine the accuracy of algorithm are below the specified threshold.

[//]: # (Image References)
[image1]: ./images/Screenshot_from_2018-02-15_16-03-22.png
[image2]: ./images/Screenshot_from_2018-02-15_16-04-40.png
[image3]: ./images/Screenshot_from_2018-02-15_16-14-48.png

---

## Instructions to run

The main program can be built and run by doing the following from the project top directory.

1. cd build
2. cmake ..
3. make
4. ./ExtendedKF
5. Open term-2 Simulator and click start 

The programs that are written to accomplish the project are present in folder src - FusionEKF.cpp, FusionEKF.h, kalman_filter.cpp, kalman_filter.h, tools.cpp, and tools.h

## Code flow

INPUT: values provided by the simulator to the c++ program

["sensor_measurement"] => the measurement that the simulator observed (either lidar or radar)

OUTPUT: values provided by the c++ program to the simulator

["estimate_x"] <= kalman filter estimated position x
["estimate_y"] <= kalman filter estimated position y
["rmse_x"]
["rmse_y"]
["rmse_vx"]
["rmse_vy"]

The estimation function process measurement is triggered when we receive new data from simulator. The data from first measurement is used to intialize the kalman filter's initial state and covariance matrices. For all the subsequent measurements, we perform prediction and measurement updates. Before prediction, time elapsed between the current and previous state is calculated. Based on the elapsed time and motion model, the new state transition and process co-variance matrices are calculated. There are two measurement update implemented in this project. If the measurement is from RADAR, which has a non-linear measurement model, we linearize the model by computing the jacobian of the measurement model and use it to calculate the kalman gain. As the measurement model for LIDAR data is linear, we can directly compute the kalman gain by skipping the jacobian formulation step. Finally, the output from process and measurement update is combined to estimate the position and covariance matrix of the object.

![alt text][image3]

## Results

![alt text][image1]

![alt text][image2]

