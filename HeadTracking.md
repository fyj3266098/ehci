# Source code #

Most updated code of a demo can be found here:
[boxView3d](http://code.google.com/p/ehci/source/browse/trunk/drafts/boxView3d/)

One can easily download this code through the following svn command:

_svn checkout http://ehci.googlecode.com/svn/trunk/drafts/boxView3d boxView3d_

# Screenshots #

Screenshots of the demo applications showing boxes according to the user head point of view.

![http://ehci.googlecode.com/svn/wiki/images/head0.jpg](http://ehci.googlecode.com/svn/wiki/images/head0.jpg)

![http://ehci.googlecode.com/svn/wiki/images/head1.jpg](http://ehci.googlecode.com/svn/wiki/images/head1.jpg)

![http://ehci.googlecode.com/svn/wiki/images/head2.jpg](http://ehci.googlecode.com/svn/wiki/images/head2.jpg)

# Videos #

Demo videos are currently hosted at youtube:

[Static Camera](http://www.youtube.com/watch?v=agxEG9NRbC0)

[Moving Camera](http://www.youtube.com/watch?v=sD0OqIdomZc)

# Model based 3d tracking #
Excelent [survey](http://www.nowpublishers.com/getpdf.aspx?product=CGV&doi=0600000001) about Monocular Model-Based 3D Tracking of Rigid Objects, by Vincent Lepetit and Pascal Fua


# LED Based Head Tracking #

DeMenthon's [paper](http://citeseer.ist.psu.edu/rd/86119495%2C110936%2C1%2C0.25%2CDownload/http://citeseer.ist.psu.edu/cache/papers/cs/5521/http:zSzzSzwww.cfar.umd.eduzSz%7EdanielzSzdaniel_papersfordownloadzSzPose25Lines.pdf/dementhon95modelbased.pdf) about head tracking could be used to track some fiducial marks, although more study should be done about it.

# Eye distance 3d tracking #

Another simple idea is to capture only the eye distance (or head height, width) and use simple tangent equations do detect the distance. Something like headDistance = focalDistance **times** (knownEyeDistanceInMM)/(pixelImageDistance)

Focus can be easily achieved through field of view. For instance, if the camera has a field of view of 45 degrees and the image is 1024 pixels large, we have (1024/2)/focusDistance = tan(45deg/2)

# Viola Jones #

Nice explanation about Viola Jones algorithm:

[http://www.ics.uci.edu/~smyth/courses/cs175/slides12\_viola\_jones\_face\_detection.ppt](http://www.ics.uci.edu/~smyth/courses/cs175/slides12_viola_jones_face_detection.ppt)

# Future direction #

I like this [idea](http://www.nvidia.com/object/3d_stereo.html) :)

Check out http://abstrakraft.org/cwiid/ , http://www.wiili.org/index.php/CWiid and http://gentoo-wiki.com/HOWTO_Use_Multimedia_Keys

# 3d distance tracking using head width #

_This code uses some approximations, but is a good starting point_

```
#include "cv.h"
#include "highgui.h"

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <assert.h>
#include <math.h>
#include <float.h>
#include <limits.h>
#include <time.h>
#include <ctype.h>

#ifdef _EiC
#define WIN32
#endif

static CvMemStorage* storage = 0;
static CvHaarClassifierCascade* cascade = 0;

//this is an approximation, for FOV = 45 degrees, 640x480 pixels
double horizontalGradesPerPixel = 53.0/640.0;
double verticalGradesPerPixel = 40.0/480.0;
double headWidth = 0.12; //supposing head's width is 12 cm 


void detect_and_draw( IplImage* image );

const char* cascade_name =
    "haarcascade_frontalface_alt.xml";
/*    "haarcascade_profileface.xml";*/

int main( int argc, char** argv )
{
    CvCapture* capture = 0;
    IplImage *frame, *frame_copy = 0;
    int optlen = strlen("--cascade=");
    const char* input_name;

    if( argc > 1 && strncmp( argv[1], "--cascade=", optlen ) == 0 )
    {
        cascade_name = argv[1] + optlen;
        input_name = argc > 2 ? argv[2] : 0;
    }
    else
    {
        cascade_name = "../../data/haarcascades/haarcascade_frontalface_alt2.xml";
        input_name = argc > 1 ? argv[1] : 0;
    }

    cascade = (CvHaarClassifierCascade*)cvLoad( cascade_name, 0, 0, 0 );
    
    if( !cascade )
    {
        fprintf( stderr, "ERROR: Could not load classifier cascade\n" );
        fprintf( stderr,
        "Usage: facedetect --cascade=\"<cascade_path>\" [filename|camera_index]\n" );
        return -1;
    }
    storage = cvCreateMemStorage(0);
    
    if( !input_name || (isdigit(input_name[0]) && input_name[1] == '\0') )
        capture = cvCaptureFromCAM( !input_name ? 0 : input_name[0] - '0' );
    else
        capture = cvCaptureFromAVI( input_name ); 

    cvNamedWindow( "result", 1 );

    if( capture )
    {
        for(;;)
        {
            if( !cvGrabFrame( capture ))
                break;
            frame = cvRetrieveFrame( capture );
            if( !frame )
                break;
            if( !frame_copy )
                frame_copy = cvCreateImage( cvSize(frame->width,frame->height),
                                            IPL_DEPTH_8U, frame->nChannels );
            if( frame->origin == IPL_ORIGIN_TL )
                cvCopy( frame, frame_copy, 0 );
            else
                cvFlip( frame, frame_copy, 0 );
            
            detect_and_draw( frame_copy );

            if( cvWaitKey( 10 ) >= 0 )
                break;
        }

        cvReleaseImage( &frame_copy );
        cvReleaseCapture( &capture );
    }
    else
    {
        const char* filename = input_name ? input_name : (char*)"lena.jpg";
        IplImage* image = cvLoadImage( filename, 1 );

        if( image )
        {
            detect_and_draw( image );
            cvWaitKey(0);
            cvReleaseImage( &image );
        }
        else
        {
            /* assume it is a text file containing the
               list of the image filenames to be processed - one per line */
            FILE* f = fopen( filename, "rt" );
            if( f )
            {
                char buf[1000+1];
                while( fgets( buf, 1000, f ) )
                {
                    int len = (int)strlen(buf);
                    while( len > 0 && isspace(buf[len-1]) )
                        len--;
                    buf[len] = '\0';
                    image = cvLoadImage( buf, 1 );
                    if( image )
                    {
                        detect_and_draw( image );
                        cvWaitKey(0);
                        cvReleaseImage( &image );
                    }
                }
                fclose(f);
            }
        }

    }
    
    cvDestroyWindow("result");

    return 0;
}

void detect_and_draw( IplImage* img )
{
    static CvScalar colors[] = 
    {
        {{0,0,255}},
        {{0,128,255}},
        {{0,255,255}},
        {{0,255,0}},
        {{255,128,0}},
        {{255,255,0}},
        {{255,0,0}},
        {{255,0,255}}
    };

    double scale = 1.3;
    IplImage* gray = cvCreateImage( cvSize(img->width,img->height), 8, 1 );
    IplImage* small_img = cvCreateImage( cvSize( cvRound (img->width/scale),
                         cvRound (img->height/scale)),
                     8, 1 );
    int i;

    cvCvtColor( img, gray, CV_BGR2GRAY );
    cvResize( gray, small_img, CV_INTER_LINEAR );
    cvEqualizeHist( small_img, small_img );
    cvClearMemStorage( storage );

    if( cascade )
    {
        double t = (double)cvGetTickCount();
        CvSeq* faces = cvHaarDetectObjects( small_img, cascade, storage,
                                            1.1, 2, 0/*CV_HAAR_DO_CANNY_PRUNING*/,
                                            cvSize(30, 30) );
        t = (double)cvGetTickCount() - t;
        printf( "detection time = %gms\n", t/((double)cvGetTickFrequency()*1000.) );
        for( i = 0; i < (faces ? faces->total : 0); i++ )
        {
            CvRect* r = (CvRect*)cvGetSeqElem( faces, i );
            CvPoint center;
            int radius;
            center.x = cvRound((r->x + r->width*0.5)*scale);
            center.y = cvRound((r->y + r->height*0.5)*scale);
            radius = cvRound((r->width + r->height)*0.25*scale);
            cvRectangle( img, cvPoint(r->x*scale,r->y*scale), cvPoint( (r->x+r->width)*scale,(r->y+r->height)*scale),colors[i%8], 3, 8, 0 ); //
	    //angle = r->width
	    double x1 = r->x*scale;
	    double x2 = (r->x+r->width)*scale;
	    
	    double angle = (r->width)*scale * horizontalGradesPerPixel * 3.141592654/180;
	    double headDist = (headWidth/2) / (tan(angle/2)); //in meters
	    double xAngle = ((img->width)/2.0 - ((r->x+r->width*0.5)*scale)) * horizontalGradesPerPixel * 3.141592654/180;
	    double headX =  tan(xAngle) * headDist;
	    double yAngle = ((img->height)/2.0 -((r->y+r->height*0.5)*scale)) * verticalGradesPerPixel * 3.141592654/180;
	    double headY = tan(yAngle) * headDist;
	    printf("HeadX = %.4lfm HeadY = %.4lfm HeadZ = %.4lfm pix %lf\n",headX,headY,headDist,(img->width)/2.0 - ((r->x+r->width*0.5)*scale));

        }
    }

    cvShowImage( "result", img );
    cvReleaseImage( &gray );
    cvReleaseImage( &small_img );
}
```