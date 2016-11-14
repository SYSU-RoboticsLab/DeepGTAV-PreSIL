# DeepGTAV
ScriptHook mod to build a vision-based deep learning environment using GTAV. It supports two main operation modes, Dataset generation or Reinforcement Learning environment (under development)

## Installation instructions
Update GTAV to the last version and just copy-paste the contents of *bin/Release* under your GTAV installation directory. Then set the correct Dataset store directory in the *config.ini* file and run the game. 

**It will work out-of-the-box, it doesn't require any extra dependencies!**

## Configuration options
The configuration options of the environment are set through the *config.ini* file:

* **mode:** 0 for dataset generation, 1 for reinforcement learning (TODO)
* **imageWidth:** Width in pixels of the images to store during dataset generation
* **imageHeight:** Height in pixels of the images to store during dataset generation
* **captureFreq:** Frequency of image and labels capture in Hz (FPS)
* **datasetDir:** Absolute path with trailing slash to directory to save the dataset (must exist)
* **maxDuration:** Duration in hours of the dataset generation
* **setSpeed:** Set speed of the vehicle in m/s during dataset generation
* **drivingStyle:** Driving style of the vehicle driver during dataset generation
* **car:** Vehicle to use during dataset generation. For now only blista (Toyota Prius) is supported (0)
* **weatherChangeDelay:** Time in seconds between weather changes
* **initialWeather:** Initial weather type
* **initialHour:** Initial in-game hour
* **initialMinute:** Initial in-game minute
* **initialPosX:** Initial x position of the vehicle (will be redefined to closest road)
* **initialPosY:** Initial y position of the vehicle (will be redefined to closest road)

## Dataset generation description
The in-game screenshots are stored as RGB PNG format, with the specified width and length of the *config.ini* file. These images are named in order of capture from 1 to undefined. Alongside the images, a file named *dataset.txt* contains a new line for each image name, with the labels associated to it separated by spaces. The labels are the following in the same order:

* Speed (m/s)
* Acceleration (m/s2)
* Brake pedal position (0 to 1)
* Steering angle (-1 to 1, left to right)
* Throttle pedal position (0 to 1)
* Yaw rate (deg/s)
* Direction (-1 to left, 1 to right)

This way of storing the dataset has two main benefits:

+ It allows easy shuffling and splitting of data, by just reordering the lines or creating new dataset files.
+ Easy preview and/or modification of the images

It can have some drawbacks also:

- Generates a lot of files, which can be hard to handle by graphical file browsers
- Higher size, given by the generation of meta-data from images and files.

## TODO
* Better describe the config options in this README file
* Finish randomizing some events, add more cars
* Find a way to automatically close/restart the game once dataset generation has finished/vehicle is stuck.
* Implement RL mode

## Acknowledgements
Many thanks to [@crizCraig](https://github.com/crizCraig) for pioneering this work with [DeepDrive](http://deepdrive.io/) and for his super valuable advices!