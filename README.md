
<!-- image -->
<div align="center" id="top"> 
  <img src=images/device.jpg width="360" />
  <img src=images/model.png width="278" />
  &#xa0;
</div>

<h1 align="center"> scanner-3d </h1>
<h2 align="center"> Lidar-based 3D environment scanner - generate a point cloud! </h2>

<!-- https://shields.io/ -->
<p align="center">
  <img alt="Top language" src="https://img.shields.io/badge/Language-Python-yellow?style=for-the-badge&logo=python">
  <img alt="Status" src="https://img.shields.io/badge/Status-in progress-red?style=for-the-badge">
  <img alt="Code size" src="https://img.shields.io/github/languages/code-size/KamilGos/scanner-3d?style=for-the-badge">
</p>

<!-- table of contents -->
<p align="center">
  <a href="#dart-about">About</a> &#xa0; | &#xa0;
  <a href="#package-content">Content</a> &#xa0; | &#xa0;
  <a href="#eyes-implementation">Implementation</a> &#xa0; | &#xa0;
  <a href="#microscope-tests">Tests</a> &#xa0; | &#xa0;
  <a href="#memo-license">License</a> &#xa0; | &#xa0;
  <a href="#technologist-author">Author</a> &#xa0; | &#xa0;
</p>

<br>


## :dart: About ##
The aim of the project is to create a device that allow to scan any sufrace to 3d model. 

The process is based on spot distance measurement. To measure the distance the lidar is used. It ensures sufficient accuracy and the range of measurements. 

The basic structure consists of a Lidar mounted on the effector of a manipulator with two degrees of freedom. The whole electronics is based on a static metal structure. The measurements are visualized in a computer application which also provides necessary operations such as Poisson reconstruction. 

<h2>Principle of operation</h2>
The manipulator consists of two degrees of freedom, each rotating by 180 degrees, which allow the measurement of the semi-spherical space above the device. The active element ensuring the rotation of each axis is a stepper motor. Measurements are performed on average every 2ms. Each time after receiving a measurement from Lidar, the microcontroller converts the obtained distance, taking into account the angular position of the effector, into Cartezian coordinate system. The angles that are used to convert the values ​​are updated with each rotation of the shaft of any motor. After the measurement process is completed, the data is transferred to a stationary station, where one make an initial decimation by removing gross errors with the help of a script. Subsequently, using an open-source program (like https://www.meshlab.net/ ), it is possible determine normal vectors for each measurement point, thanks to which we are able to use Poisson smoothing to reconstruct the measurement surface.

<br>

<div align="center" id="top"> 
  <img src=images/model.gif width="500" />
  &#xa0;
</div>

<br>

## :package: Content
 * [CAD/3d_printing](CAD/3d_printing) - STL files for 3d-printing
 * [CAD/sacnner.stp](CAD/scanner.stp) - STEP file with model
 * [examples](examples) - two exmaple files with point clouds genereted with described device
 * [schematic](schematic) - pdf and sch schematics of electronics model
 * [sources](sources) - code for microcontroller

## :eyes: Implementation ##
The mapping algorithm can be explained in the following way:

1. The upper motor takes steps until the upper limit switch sends a signal to the microcontroller. It goes back and performs micro-steps until the upper limit switch sends a signal to the microcontroller for precise alignment.
2. The lower motor does the same as the upper motor for the lower limit switch.
3. The lower motor performs 1 micro step.
4. The top motor performs 1 micro step.
5. Lidar takes a distance measurement and sends it to the microcontroller.
6. Converting distances to coordinates (x, y, z) in the microcontroller
7. The upper motor carries out the remaining micro-steps by performing steps 5 and 6 of the algorithm.
8. Measurements are saved on the SD card in the format (x, y, z).
9. The lower motor carries out the remaining micro-steps by performing steps 3-8

## :microscope: Tests ##
Many scans have been performed, which indicate that the device makes sense and its further development may bring beneficial results. The scans from the examples folder are presented below:

<h2>Example 1 - part of room<h2>
<div align="center">

| Name   | Figure    |
|--------------- | --------------- |
| Real view  |   <img src=images/real.jpg width="400" />  |
| Points cloud  |   <img src=images/points_cloud.png width="400" />  |
| Poisson reconstruction  |   <img src=images/mesh.png width="400" />  |
| Ball pivoting reconstruction|   <img src=images/mesh_ball_piv.png width="400" />  |

</div>

<h2>Example 2 - whole room<h2>
<div align="center">

| Name   | Figure    |
|--------------- | --------------- |
| Points cloud |   <img src=images/points_cloud2.png width="400" />  |


</div>


## :memo: License ##

This project is under license from MIT.

## :technologist: Author ##

Made with :heart: by <a href="https://github.com/KamilGos" target="_blank">Kamil Goś</a>

&#xa0;

<a href="#top">Back to top</a>