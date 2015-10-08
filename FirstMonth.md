# Blog Posts #

http://danielbaggio.blogspot.com/2008/05/ehci-update.html

http://danielbaggio.blogspot.com/2008/06/ehci-updates-this-week-ive-been-working.html

http://danielbaggio.blogspot.com/2008/07/ehci-upate-6-degrees-of-freedom-head.html

# Videos #

[3d Head tracking without Wiimote - Camera view](http://www.youtube.com/watch?v=sD0OqIdomZc)

[3d Head tracking without Wiimote - Both views](http://www.youtube.com/watch?v=agxEG9NRbC0)

[Hand gesture letter 'A'](http://www.youtube.com/watch?v=o1WNb0g0f9Q)

[Hand tracking using HandVu](http://www.youtube.com/watch?v=Rmh-mZFxWns)

[6 dof head tracking](http://www.youtube.com/watch?v=M8EigZxdk1o)

[Updated 6 dof head tracking](http://www.youtube.com/watch?v=M5kqgBO6D9s)


# Source Code #

[6dofhead.cpp](http://code.google.com/p/ehci/source/browse/trunk/drafts/6dofhead/6dofhead.cpp)

[6 Degrees of Freedom head tracking files](http://code.google.com/p/ehci/source/browse/trunk/drafts/6dofhead/?r=38)

[boxView3d.cpp](http://code.google.com/p/ehci/source/browse/trunk/drafts/boxView3d/boxView3d.cpp)

[BoxView files](http://code.google.com/p/ehci/source/browse/trunk/drafts/boxView3d/?r=38)

# Documentation #

[6 Degrees Of Freedom HeadTracking](http://code.google.com/p/ehci/wiki/6dofhead)

[Head Tracking](http://code.google.com/p/ehci/wiki/HeadTracking)

[Hand Tracking](http://code.google.com/p/ehci/wiki/HandTracking)



# Achievements and Future planning #

From the original planning, several deliverables for the 2nd month have been already done, while some from the 1st month have been skipped. The reason for this skipping was that working with the head seemed a little bit easier than with hands, this way, more background was acquired with the simpler task, so that the harder one can be addressed with more experience on the algorithms. The original schedule was:

1st Month:
> ~~Hand tracking~~ and hand gesture recognition classes. Zoom and rotation features. Documentation of classes through tutorials, code documentation and demos.

2nd Month:
> ~~Head~~ and body tracking facade classes. ~~3D head tracking class~~. Documentation and ~~small OpenGL demos~~.

3rd Month:
> Motion flow and 3d model wireframe tracking classes. Documentation. Project packaging through Google Summer of Code and Natural User Interface sites.


The rescheduled plan could be:

1st Month:
> ~~Hand and Head tracking~~. ~~3D head tracking class~~. ~~Small OpenGL demos~~.

2nd Month:
> Body tracking, and gesture recognition classes. Zoom and rotation features. Documentation of classes through tutorials, code documentation and demos

3rd Month:
> Motion flow and 3d model wireframe tracking classes. Documentation. Project packaging through Google Summer of Code and Natural User Interface sites.

For the next weeks, I intend to finish the 6dof head tracking so that automatic initialization in any position is achieved, and also decrease jittering through the use of more points.

Besides finishing the sample program, some work needs to be done in order to separate demo functionalities from ehci library functionalities, so that reuse can be done.

As soon as the 6dof head tracking is finished, 2nd month deliverables will be focused.