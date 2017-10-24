# Extrinsic calibration

This a short tutorial for extrinsic calibration of Pepper's Depth and
RGB cameras.

## Setup

First of all, print a calibration pattern (a chessboard) if you do not
have any. We would recommend A3 size. Once you have it, count the
number of rows and columns and measure a size of a square. Adjust
these parameters in the launch file
calibration_cameras/launch/calibration_cameras_pepper.launch (you
should provide the numbers of rows and columns -1 because you need the
number of crossings rather than rows and columns).

## Data recording

- wake up your robot and move the head to the "zero position" (setting
  all joints to zero, for example in Choregraphe)
- create an empty folder for data recording and set its name in the
  same launch file
- launch the code: roslaunch calibration_cameras
  calibration_cameras_pepper.launch
- place the calibration pattern in front of the robot
- once the pattern is detected (you can see all detected crossings),
  press "s" on your keyboard to save images from both cameras
- repeat 2 previous steps each time changing a distance and/or an
  angle to cover different views (at 60cm-80m) until you reach a
  sufficient number of image pairs (for example, 30 times or more)

## Calibration based on recorded data
- launch the code to compute extrinsic parameters based on recorded
  images: roslaunch calibration_cameras
  calibration_cameras_pepper.launch
- press "c" on your keyboard to compute calibration values
- check if the resulted XYZ and RPY for last processed image pair
  correspond to the reality

The extrinsic parameters obtained for our Pepper are:

```
XYZ: 0.0708098 0.02 0.118115
RPY: -1.5936 -0.0161345 -1.57777
```

How to update the extrinsic parameters in URDF of your robot:
- update the values in URDF like here: https://github.com/nlyubova/pepper_robot/commit/b973bf1ccbd190a6a7fb19e24f7cf9114e0bdcae
- copy the pepper.urdf file to catkin_ws/src/naoqi_driver/share/urdf/ (and replace the existing one)