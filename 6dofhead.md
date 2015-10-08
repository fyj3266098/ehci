## Source code ##

The code is still under development but a preview is available from the svn http://code.google.com/p/ehci/source/browse/trunk/samples/6dofhead.cpp

# Introduction #

This part of the project deals with head tracking with 6 degrees of freedom, a problem often referred as finding the pose of an object. Since no light is being generated from the head - as in some types of infra-red tracking - it needs to rely on natural features of the head.

This implementation tries to follow the excellent work from Luca Vacchetti, Vincent Lepetit, and Pascal Fua, from the Computer Vision Laboratory of the Swiss Federal Institute of Technology (EPFL), "Fusing Online and Offline Information for Stable 3D Tracking in Real-Time". The paper is available [here](http://cvlab.epfl.ch/~vlepetit/papers/vacchetti_cvpr03.pdf)

[![](http://ehci.googlecode.com/svn/wiki/images/6dof.jpg)](http://www.youtube.com/watch?v=M5kqgBO6D9s)

There's a video on [youtube](http://www.youtube.com/watch?v=M5kqgBO6D9s) showing current progress.


# Details #

The algorithm starts automatically looking for a head in the image, through the famous [Viola Jones](http://en.wikipedia.org/wiki/Robust_real-time_object_detection) algorithm.

After finding the head position, a feature tracking algorithm is started. It uses cvFindGoodFeatures to track in the region of interest defined by the head width and height. When these features are discovered, they are mapped back to a head model (I'm currently using a cylindrical model, but I plan to use the excellent head model by Len [Van Der Westhuizen](http://www.lenwest.org/), which is available [here](http://blenderartists.org/forum/showthread.php?t=103053), thanks Len!).


![http://ehci.googlecode.com/svn/wiki/images/blender.jpg](http://ehci.googlecode.com/svn/wiki/images/blender.jpg)

_Here, Len's head is being edited in blender_

When the head model 3d points are known, as well as its corresponding 2d image points, DeMenthon's [POSIT algorithm](http://www.cfar.umd.edu/~daniel/Site_2/Code.html) is used to find the initial pose estimation.

After that, an optical flow [algorithm](http://en.wikipedia.org/wiki/Lucas_Kanade_method) by Lucas-Kanade is used is used to track the points along the frames. These points are mapped back to original 3d points and the pose matrix is updated.

# Links #

Posit tutorial:
http://opencvlibrary.sourceforge.net/Posit

Explanation of the raw format:
http://local.wasp.uwa.edu.au/~pbourke/dataformats/povraw/

Documentation of gluPerspective (used to determine OpenGL projection matrix)
http://www.opengl.org/sdk/docs/man/xhtml/gluPerspective.xml

Another good idea would be to use something like CMU's [paper](http://www.cs.cmu.edu/~face/Papers/IJIST_headmotionrecovery.pdf)

# TODO #

This project is functional, but it could receive some enhancements.

The first thing to take in consideration is the RANSAC algorithm, currently, outliers are kept and this increases the error in long sequences, which makes reinitialization required.

Another enhancement is to exchange the sine head model with the actual head model and use the facet id concepts.

## Some personal notes (in Portuguese) ##

RANSAC com keyframe:

Dado o frame inicial (keyframe) e o atual, faz-se o Lucas-Kanade. Mapeia-se os pontos M originais com os m do frame atual.
Utiliza-se o RANSAC:
> - sorteia-se um conjunto de pontos m e faz-se o POSIT. Utiliza-se o keyframe inicial (como textura sobre o head model ou sobre o cilindro) e projeta-se com a matriz obtida pelo POSIT. Faz-se a medida de erro (não sei qual é melhor/sugerida, pois podem ser duas: distância (x,y) entre os pontos projetados pela matriz e os pontos m, ou a distância dos pixels de um quadrado reprojetado... talvez a primeira). Ao longo do Posit, pode-se pegar mais pontos, considerados inliers, caso eles dêem o fit. Chega-se a um RT para estes pontos.
> - sorteia-se novos pontos, repetindo o processo. Mantém-se o melhor resultado.

Combinando-se com o online: faz-se ramsac com keyframe, depois, faz-se RANSAC com os pontos identificados entre o último frame e o atual. Caso eles não se ajustem ao atual são removidos e caso contrário entram para cooperar com o melhor RANSAC.

Mais detalhes sobre o RANSAC no multiple view geometry.

Algoritmo do CMU:

1- Extrair template da cara a partir de uma inicialização como no Viola-Jones frontal.

2- Encontrar uma região que minimize o erro entre o ?quadrado? inicial e a nova região. Para calcular o erro, utiliza-se um peso para os pixels, que é função da densidade (pixels que estão na normal da câmera têm peso maior) e o gradiente (pixels com gradiente alto ou próximo têm peso maior). Além disso, pixels com diferenção muito grande(prováveis outliers) são amortecidos por uma exponencial.

3- Encontrada a região, calcula-se a matriz de rotação/translação.

... por que o método é incremental?! ... como varrer a nova tela?...
Na verdade



O template tem sempre o mesmo tamanho. Lembre-se que ele é da figura 3d criada.