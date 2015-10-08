# EHCI 6 degrees of freedom hand tracker #

![http://ehci.googlecode.com/svn/wiki/images/handTracking.jpg](http://ehci.googlecode.com/svn/wiki/images/handTracking.jpg)

For a video showing the algorithm, check:

http://www.youtube.com/watch?v=BEMEeCDJ-3I

http://www.youtube.com/watch?v=JhPDEviPZXI

# Comparing algorithms #

## Viola-Jones ##

![http://ehci.googlecode.com/svn/wiki/images/viola.jpg](http://ehci.googlecode.com/svn/wiki/images/viola.jpg)

This [video](http://www.youtube.com/watch?v=o1WNb0g0f9Q) shows the use of a Viola-Jones HaarCascades detector developed by Juan Wachs (more info [here](http://www.bgu.ac.il/~juan/index_files/Publications.html)).
This detector is only supposed to detect closed hands, like the [A gesture](http://en.wikipedia.org/wiki/American_Manual_Alphabet) from American Manual Alphabet  features. I'm running the OpenCV Haarcascades with a scale of 3 and detection time is around 11 ms.
This detector shows robust behaviour when presented with natural backgrounds like wardrobes and walls from my room. It does not seem to work well when the hand is near the face (near HSV maybe?). The training of the classifier must also include images with this condition.

For more information about this algorithm, refer to the great paper [http://www.merl.com/reports/docs/TR2004-043.pdf Rapid Object Detection Using a Boosted
Cascade of Simple Features]

## Flock of features ##

![http://ehci.googlecode.com/svn/wiki/images/handvu.jpg](http://ehci.googlecode.com/svn/wiki/images/handvu.jpg)

This other [video](http://www.youtube.com/watch?v=Rmh-mZFxWns) shows [HandVu](http://www.movesinstitute.org/~kolsch/HandVu/HandVu.html) approach.
This algorithm is based on the paper [Fast 2D Hand Tracking with Flocks of Features](http://www.movesinstitute.org/~kolsch/handvu/KolschTurk2004Fast2DHandTrackingWithFlocksOfFeatures.pdf).
This algorithm tracks several sides of the hand, and, if nothing too much similar to the hand is on the way, a good tracking is achieved. Besides that, HandVu is a very mature software.