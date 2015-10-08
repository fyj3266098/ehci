_Observation: one might need to add this in case python does not recognize where ehci.py is_

export PYTHONPATH=/usr/local/lib/python2.5/site-packages/

# Introduction #

This sample shows how to obtain head bounds after library initialization.

```
import ehci

ehci.ehciInit()

while(1):
	ehci.ehciLoop(1,0)
	x,y,width,height = ehci.getHeadBounds()
	print "Coord (",x,",",y,") width ",width,"height ",height
```

Save the above code in a file called simple.py and run it through

```
python simple.py
```

You should see your webcam output with a rectangle around your head and some text output like:
```
Coord ( 262 , 128 ) width  182 height  182
Coord ( 268 , 128 ) width  184 height  184
Coord ( 276 , 128 ) width  184 height  184
Coord ( 282 , 126 ) width  190 height  190
Coord ( 288 , 128 ) width  186 height  186
Coord ( 294 , 130 ) width  182 height  182
Coord ( 294 , 128 ) width  186 height  186
Coord ( 304 , 132 ) width  172 height  172
Coord ( 304 , 132 ) width  176 height  176
Coord ( 302 , 130 ) width  176 height  176
Coord ( 306 , 136 ) width  172 height  172
```