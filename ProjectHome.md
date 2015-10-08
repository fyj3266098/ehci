_ehci can also be used as an open source head tracking library_

[![](http://google-summer-of-code.googlecode.com/files/soc08-198x128_white.jpg)](http://code.google.com/soc/2008/)
[![](http://ehci.googlecode.com/svn/wiki/images/logo_ita.gif)](http://www.ita.br/)
[![](http://ehci.googlecode.com/svn/wiki/images/nuilogo.gif)](http://www.natural-ui.com/) <a href='http://www.youtube.com/watch?feature=player_embedded&v=BovphSjw_tI' target='_blank'><img src='http://img.youtube.com/vi/BovphSjw_tI/0.jpg' width='425' height=344 /></a>


# Potential Applications #

IdeAs - Please Contribute

# News #
# 03/06/13 - Please, consider checking chapter 6 source code from the book Mastering OpenCV with Practical Computer Vision Projects [here](https://github.com/MasteringOpenCV/code) #

07/20/10 - New release 0.7. Bug fixes. In development environment the program hasn't crashed so far. Corrections in RANSAC iteration have been done. Please download the latest [release](http://code.google.com/p/ehci/downloads/detail?name=ehci-0.7-windows-binary-samples.zip&can=2&q=) and submit issues.

06/15/10 - Added windows binaries for easier software evaluation, check Downloads section

12/18/09 - We are on Linux Magazine

Alessandro Faria has published a cool article about EHCI on December issue of Linux Magazine. [Check it here!](http://lnm.com.br/images/uploads/pdf_aberto/LM_61_52_55_04_tut_visao.pdf)

03/28/09 - Planning

Reading the survey from Erik Murphy-Chutorian http://cvrr.ucsd.edu/publications/2009/MurphyChutorian_Trivedi_PAMI09.pdf and planning new directions for EHCI.


02/28/09 - New release EHCI 0.6
New features
  * RANSAC - RANdom SAmple Consensus algorithm filters outliers yielding more stable results.
  * Configure file - the config.ini file makes room for selecting the camera as well as using input from files
  * Better model positioning

02/12/08 - Some research
  * After reading lots of papers, here is the conclusion for NextSteps

02/11/08 - Next steps
  * Refactor code
  * Use RANSAC for good in keyframes

12/26/08 - Some milestones reached!

RANSAC is now done, thanks to God (check not calibrated video [here](http://www.youtube.com/watch?v=nh_yVz_kPr4)), but still needs to:
  * ~~Adjust sinusoidal model to glue to face in the reference point~~
  * ~~Delete RANSAC outliers~~
  * Adjust RANSAC paramters
  * ~~Use a config file (for the camera and other parameters)~~
  * Decouple the head model used (make room to use other models)
  * Optimize some code
  * Use headmodel instead of sinusoidal
  * Use keyframes to zero error accumulation
  * Capture features
  * Create a blender plug-in
  * X-Server integration (XGl)
  * Integrate with compiled OpenCV 1.1 version
  * Test vinjn.z binaries and check windows binaries
  * ~~Work with videos for functional testing~~


[![](http://pyconbrasil.com.br/logo.png)](http://pyconbrasil.com.br)

09/20/08 - PyCon Brasil 2008
  * Queria deixar o meu grande agradecimento a todos da PyCon Brasil 2008, pelas excelentes palestras, pela organização e pelas grandes pessoas que pude conhecer lá. Meus sinceros agradecimentos a vocês!
  * [Slides da PyCon 2008](http://ehci.googlecode.com/files/PyCon2008.pdf)


09/17/08 - New Release:
  * EHCI 0.5 with Python bindings has been released. Check out Panda3D integration sample.

09/13/08 - Next milestones:
  * ~~Python bindings~~
  * ~~RANSAC algorithm~~

# Documentation #

## Installation ##

InstallingOnLinux

CompilingOnWindows

ConfigIni

## Diagrams ##

ActivityDiagram

## Project research and reports ##

[Python Interface](Swig.md)

[6 Degrees Of Freedom HeadTracking](6dofhead.md)

HeadTracking

HandTracking

ChromaKeying

## Tutorials ##

[Getting head position, width, and height](simple2d.md)

[Obtaining head X, Y, and Z coordinates](simple3d.md)

[Python interface tutorial](pyehci.md)

# Project description #

This application is a webcam image processing library on top of OpenCV intended to generate events from user's head, hand and body movements. This library is also intended to track objects so that augmented reality can be made. In order to enhance human computer interaction, the application is going to use a single webcam, without the needs to use FTIR or Diffused Illumination techniques. Besides tracking positions, this library will also be able to provide higher level events and gestures like get 3d user position, and open hand gestures. Collision with virtual objects is also considered in augmented reality.

## Features: ##
2d/3d head tracking, hand/finger tracking, body tracking, gesture recognition, fiducial marks, motion velocity, augmented reality object tracking.

Aligned with Natural User Interface idea of benefiting artistic and educational applications, this library's use could range from helping people severely paralyzed or afflicted with diseases such as ALS (Lou Gehrig’s disease) to revolutionary user interface paradigms. 3d head-tracking can create an environment so that Internet browser contents could be zoomed in and out as well as visualize 3d models from user perspective of view. Hand and finger tracking can be used in eye-toy like games as well as scrolling book pages or photos from distance, as when showing photos to friends or in Slideshow  presentations. Similar functionalities like Touchlib's could also be used. Augmented reality can bring a brand new revolutionary paradigm of user interface through an unexplored mix of virtual and real objects for never seen interaction mechanisms. Library demo applications like these should be included. An interesting trait of this library is that users won't need to wear any equipment!

## Brief list of deliverables: ##

1st Month:
> ~~Hand tracking~~ and ~~hand gesture recognition~~ classes. Zoom and rotation features. ~~Documentation of classes through tutorials, code documentation and demos~~.

2nd Month:
> ~~Head~~ and body tracking facade classes. ~~3D head tracking class~~. ~~Documentation~~ and ~~small OpenGL demos~~.

3rd Month:
> Motion flow and 3d model wireframe tracking classes. ~~Documentation~~. ~~Project packaging through Google Summer of Code~~ and Natural User Interface sites.

Pdf describing the application:
http://gpuwire.googlecode.com/files/SoCProposal.pdf


---

## Reports ##

FirstMonth

[Final Report](http://danielbaggio.blogspot.com/2008/08/ehci-final-report.html)