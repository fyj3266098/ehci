**Python bindings have been successfully implemented check [[InstallingOnLinux](InstallingOnLinux.md)] for more information**

Python bindings work through shared objects that are compiled with help from SWIG. These libraries implement some init function. They are named with the `_` prefix. This way, ehci library is imported from some `_ehci.so` dynamic library.

According to [python install instructions](http://docs.python.org/inst/standard-install.html) the `_ehci.so` files should go to some directory like /usr/local/lib/python2.5/site-packages or to the same directory in which the user is.

In order to make the right coupling between the library and python, the interface file, ehci.i should be properly modified.

Compiling dynamic library on Linux
```
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig/
swig -c++ -python ehci.i
g++ -c ehci_wrap.c ehci.cpp -I /usr/include/python2.5/ `pkg-config opencv --cflags
g++ -shared ehci.o ehci_wrap.o -L /usr/local/lib/ -lGL -lglut -lcv -lhighgui -lcvaux  -lml -lcxcore -o _ehci.so
python
import ehci

```

# Links #

[Swig tutorial](http://www.swig.org/tutorial.html)

[Swig Autoconf](http://www.geocities.com/foetsch/python/swig_linux.htm)

[Using typemaps](http://projects.scipy.org/scipy/numpy/browser/trunk/numpy/doc/swig/doc/numpy_swig.html?format=raw)