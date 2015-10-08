# Combining online and offline information #

The great problem right now is getting rid of error accumulation, which seems to be possible using the keyframe approach.

Well, reading the paper "Fusing Online and Offline Information for Stable 3D Tracking in Real-Time", Vacchetti, Lepetit, Fua, the following procedure is used to combine information from keyframe and previous tracked frame:

"In our approach we therefore attempt to combine the
strengths of both the online and offline information as follows:
first, we match the current frame with the chosen
keyframe and apply RANSAC to the set of points we found,
discarding the outliers and retaining a set of points Mk
free from error accumulation. Then, we perform a modified
RANSAC estimation over the matches between the current
frame with the previous one: if an [R,T] sample tested
by the RANSAC estimator rejects some points in Mk
, this
sample is not considered by this second stage. This way,
this stage estimates the values [R,T] using all the points in
Mk
, which provide reliable but partial information, and the
matches between the previous and the current frames that
provide additional information."

Reading their following paper, the combination of information is more mathematically elaborated, yielding to the bundle adjustment problem, which seems to use the Levenberg-Marquardt algorithm, which is basically a least-squares for non-linear functions (as is the case of the projection error). The implementation of Levenberg-Marquardt seems to have been already made in Gnu Scientific Library. Checking "Multiple-View Geometry" bundle adjustment chapter and the paper "Model-Based Bundle Adjustment with Application to Face Modeling" are also good ideas to see if this is the correct way to go.

For now, the simpler approach of "Fusing Online and Offline Information for Stable 3D Tracking in Real-Time" will be used. If it does not yield good results, this other more formal approach will be implemented.

ps: Should take a closer look at http://www.thepixelfarm.co.uk/ PFTrack