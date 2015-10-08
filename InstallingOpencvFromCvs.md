# Installing OpenCV from CVS #

OpenCV library is available from sourceforge repositories, at http://sourceforge.net/projects/opencvlibrary/ . When this install file was written, there was no package from version 1.1 available for download. So the best way to get it, is through a CVS checkout.
In order to do so, issue the following commands (you need to have cvs installed in your machine):

```
cvs -d:pserver:anonymous@opencvlibrary.cvs.sourceforge.net:/cvsroot/opencvlibrary login
```

When asked for a password, simply press enter. And then:

```
cvs -z3 -d:pserver:anonymous@opencvlibrary.cvs.sourceforge.net:/cvsroot/opencvlibrary co -P opencv
```

This will checkout files from the very last development version. In order to build and install opencv, you should look for the file opencv/INSTALL, but, in case you have the required libraries:

  * GTK+ 2.x or higher including headers
  * pkgconfig
  * libpng, zlib, libjpeg, libtiff, libjasper with development files.
  * Python 2.3, 2.4 or 2.5 with headers installed (developer package)
  * libavcodec, etc. from ffmpeg 0.4.9-pre1 or later + headers.
> > Earlier versions do not work with OpenCV because of different API.
> > libavcodec is LGPL software, so to use it with non-GPL software (such as OpenCV)
> > you need to build and use a _shared_ library libavcodec.so.**:
> > > get ffmpeg from ffmpeg.sourceforge.net
> > > ./configure --enable-shared
> > > make
> > > make install
> > > you will have got: /usr/local/lib/libavcodec.so.**
> > > > /usr/local/lib/libavformat.so.**> > > > (/usr/local/lib/libavutil.so.** for newer versions)
> > > > > /usr/local/include/ffmpeg/**.h**


> You can build it with a simple:

```
./configure
make
```

As super user:
```
make install  
/sbin/ldconfig
```

And then, watch out for this installation note:
"default installation path is /usr/local/lib and /usr/local/include/opencv,
> so you need to add /usr/local/lib to /etc/ld.so.conf (and run ldconfig after)
> or add it to LD\_LIBRARY\_PATH environment variable"