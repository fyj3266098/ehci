# Compiling on VisualStudio #

Updated for Ehci-0.7

  1. Download and install CMake: http://www.cmake.org/
  1. Open the cmake-gui
  1. On the "Where is the source code:" point to the place where you have downloaded and extracted ehci-0.7 source (find it here http://ehci.googlecode.com/files/ehci-0.7-src.zip in the downloads section, I have just updated)
  1. On the "Where to build the binaries:" choose your preferred place to generate solution files
  1. Click "Configure" and choose your installed compilers, and then Finish
  1. Chances are you'll get an error in configuration process. It's ok, let's fix it
  1. CMake hasn't found your directories for OpenCV and GLUT. For OpenCV, just browse to it, in case you have it installed. Else, go to sourceforge and grab it, install, and then point to it... it's usually at "C:/OpenCV2.1"
  1. For GLUT, on windows, you will need to point to Nate Robins binaries (google for Nate Robins glut), http://www.xmission.com/~nate/glut.html . Download and extract the bin version. And then, point GLUT\_INCLUDE\_DIR to Downloads/glut-3.7.6-bin/glut-3.7.6-bin and GLUT\_LIBRARY to Downloads/glut-3.7.6-bin/glut-3.7.6-bin/glut32.lib
  1. Check the "Build\_opengl\_samples" for some fun
  1. Hit configure again... you'll see some warnings and then something like: "Looking for GLUT Looking for GLUT - found : C:/Documents and Settings/Administrator/My Documents/Downloads/glut-3.7.6-bin/glut-3.7.6-bin Configuring done"
  1. Well done, hit "Configure" again, and then "Generate". You should see: "Generating done"
  1. Congratulations, now you have all the solution files (in case you are with Visual Studio) so you can open then and change them as you wish. Go to "\ehci-build\samples" and open the boxView3d.vcproj, for instance. Click "Build->Build Solution" and Visual Studio should generate the executables on "ehci-build\samples\Debug". You should just go there and double click boxView3d.exe, for instance. And then, you might get something like: "This application has failed to start because cxcore210d.dll was not found". It means your opencv dlls are not on the path... a fast way to find them is copying all dll files from "C:\OpenCV2.1\bin" to your ehci-build\samples\Debug" folder.
  1. Double click them again and then... oops, glut32.dll might also be missing. Just copy it there as well (or send to your system32). Remember that it comes from Nate Robins glut binaries, there's a file at "glut-3.7.6-bin\glut-3.7.6-bin\glut32.dll".
  1. Almost there... now your executable is looking for data files... which are back in your ehci source folder: "\ehci\data". Just copy the whole directory to your samples\Debug and then... almost there... your data\config.ini might be trying to open some trash. Just make sure it looks like this:

---

USE\_RANSAC 1
RANSAC\_SAMPLES 6
RANSAC\_DISTANCE\_THRESHOLD 30.0
RANSAC\_ITERATIONS 20
CAMERA\_INDEX 1
OPEN\_MOVIE NO

---

Edit and save it, go back to boxview3d.exe and double click it :)
Voilà... you should see the 3d cube moving as your head moves. Check out the other samples, make changes and write back in case you had any other problems.


_These are vinjn.z (http://code.google.com/u/vinjn.z/)  instructions to compile on windows_

I'm also using VisualStudio, in order to compile, the following 3 files needs to be
included to an empty win32 console project
ehci-0.5\lib\ehci.h
ehci-0.5\lib\ehci.cpp
ehci-0.5\samples\boxView3d.cpp (other samples also work, but this one is cool!)

also remeber to setup the OpenCV environment
```

#ifdef _DEBUG
	#pragma comment(lib,"cvd.lib")
	#pragma comment(lib,"cvauxd.lib")
	#pragma comment(lib,"cxcored.lib")
	#pragma comment(lib,"highguid.lib")
#else
	#pragma comment(lib,"cv.lib")
	#pragma comment(lib,"cvaux.lib")
	#pragma comment(lib,"cxcore.lib")
	#pragma comment(lib,"highgui.lib")
#endif
```

GoodLuck!