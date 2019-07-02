# Road lane detection Project
---

I'm sorry, just after I submitted the project, a nasty bug was discovered in project_video_combined.mp4 since 0:35

## 1. Getting camera intrinsic parameters
    
    To recovery distortion it's need to calibrate a camera:
    give calibration set of images (chess patterns) and localize corners on every image if it's available.
    solve PnP problem for n = 3 due to calling OpenCV calibrateCamera() function
    compute intrinsic matrix and distortion coefficients.
    
    Calibration images set is in camera_cal/ directory, and result (matrix k and vector dist) has been saved
    in two files k.yaml and dist.yaml
    
    Test image pair is placed in examples/undistorted.png
    <img> src='examples/undistorted.png'</img>
    
## 2. Calculate extrinsic camera parameters (like a R,t matrix)
    
    In this project it is enough to perform 2D-2D transformation with 4 pairs of point coordinates.
    I found a straight road section and marked 4 points onto both lines so upper and lower sides that trapeze are horizontal. Then I turn this trapeze around its footing and make it to be rectangle. These are a new points to transform whole image.

    Example of transformed image is placed in examples/unwarped_pair.png
    <img> src='examples/unwarped_pair.png'</img>
    
## 3. Image binarization

    This is a key point of this project because mishit on this stage will very hardly to recover later.
    I use a red component of RGB triplet to threshold it to binary image.
    I also tried different filters with stairs-like kernel and so on, but it was not so effective.

## 4. Road Lines localization and approximation
    
    In this section of the project I use the code from the relevant lessons.
    But I have a serious problem with the calculation of curvature. It seems the reason is in scaling pixels to meters because everything else is identical. I even had to use a hint from one of the students (function measure_curvature_offset (), scaled_* values), but it didn't help me. The curvature is still calculated as Inf.
    
## 5. Video zoom
    
    Finally, it needs to decorate the video to mark the road lane. This code is simple and has also been taken from the video tutorials.
     Output video (with postfix _combined) is placed to same directory as an input one.