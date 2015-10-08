# Installation instructions for EHCI 0.x #
_important: you should replace 0.x for the version you are using, for instance, 0.3_

In order to install the library, download the last distribution release of EHCI through the download tab, go to the directory in which you've copied the ehci-0.x.tar.gz and issue the following commands:

```
tar xvfz ehci-0.x.tar.gz
cd ehci-0.x
./configure
make
```

**if you want to build python bindings do the following instead**

_Python bindings are only available from EHCI 0.5 on_

```
tar xvfz ehci-0.x.tar.gz
cd ehci-0.x
./configure --enable-pyehci
make
```


Now, log as super user, go to the ehci-0.x directory and run:
```
make install
```

This is the explanation of the commands:

```
tar xvfz ehci-0.x.tar.gz   # unpack the sources
cd ehci-0.x                # change to the toplevel directory
./configure                # run the `configure' script
make                       # build EHCI
make install               # install EHCI
```


As the OPENCV library is required for you to install EHCI, you might get this error while running ./configure:

"checking for OPENCV... configure: error: Package requirements (opencv >= 1.1.0) were not met:

No package 'opencv' found

Consider adjusting the PKG\_CONFIG\_PATH environment variable if you
installed software in a non-standard prefix."

This means you don't have opencv 1.1.0 or higher installed in your machine. Refer to the topic InstallingOpencvFromCvs. You might as well receive the following error:

"checking for OPENCV... configure: error: Package requirements (opencv >= 1.1.0) were not met:

Requested 'opencv >= 1.1.0' but version of OpenCV is 1.0.0

Consider adjusting the PKG\_CONFIG\_PATH environment variable if you
installed software in a non-standard prefix.

Alternatively, you may set the environment variables OPENCV\_CFLAGS
and OPENCV\_LIBS to avoid the need to call pkg-config.
See the pkg-config man page for more details."


This means you have OpenCV installed, but your version is 1.0.0. This might be the case when you install it from the sourceforge downloadable package, opposed to checking it out from the cvs. In case you've received this error, look for the topic InstallingOpencvFromCvs.


# Running samples #


In case there weren't errors, you should be able to go to the directory /usr/local/share/ehci/samples and run the samples that come with the library. In order to run the 6 degrees of freedom sample do the following:

```
cd /usr/local/share/ehci/samples
./6dofhead
```

This should run the 6dofhead demonstration sample (it will track translation and rotation of your head, you should be looking toward your webcam in order for it to start). In case it won't run, you might get the following error message:

```
./6dofhead: error while loading shared libraries: libehci.so.0: cannot open shared object file: No such file or directory
```

This means that your system cannot load the library because it is not in the default places it is looking for (usually /usr/lib), but you might check that your library, libehci.so is located at /usr/local/lib/libehci.so . The easy fix, is to tell your system about it through the following command:

```
export LD_LIBRARY_PATH=/usr/local/lib
```

And then, try and run the program again through:

```
./6dofhead
```

This will most probably work, but the best way to tell your system about this new library is adding it to the /etc/ld.so.conf file. In order to do this, as a super user, edit the file /etc/ld.so.conf and add this line to it:

```
  /usr/local/lib/
```

And then run, as super user, run:

```
/sbin/ldconfig
```

This will add the library to the cache and you won't need to alter the environment library LD\_LIBRARY\_PATH again.


_Notice to run python demos, the 6dof.py, you might need to do this export firstly_

export PYTHONPATH=/usr/local/lib/python2.5/site-packages/

# Contributors procedures #

If you want to contribute with EHCI code, you'll firstly need to checkout files from [svn](http://code.google.com/p/ehci/source/checkout), and then, run the following command:

```
autoreconf --install
```

It will generate Makefiles so that it can be configured and installed. In order to create a new distribution tarball, the following command should be issued:

```
make dist
```