# Visual Odometry Pipeline (Python 3 Optimized)

This project implements a Visual Odometry (VO) pipeline in Python 3, optimized from an original Python 2 version. The code uses stereo camera images to estimate the position and orientation of a moving camera over time. The implementation leverages feature tracking and pose estimation to compute camera trajectories.

This work is based on the original repository by [uoip](https://github.com/uoip/monoVO-python), which has been adapted and optimized for Python 3 compatibility.

## Contents

- **`test.py`**: Main script to run the visual odometry process.
- **`visual_odometry.py`**: Defines classes and functions for visual odometry computation.

## Features

- **Feature Tracking**: Uses the Lucas-Kanade optical flow method to track feature points between consecutive frames.
- **Pose Estimation**: Estimates the camera's motion using the Essential Matrix and pose recovery techniques.
- **Pinhole Camera Model**: Simple pinhole camera model with support for distortion correction.
- **Trajectory Visualization**: Visualizes the estimated trajectory against the ground truth trajectory.

## Installation

### Requirements

This project uses the following Python libraries:

- `numpy`
- `opencv-python`

To install the dependencies, run:

```bash
pip install numpy opencv-python
```

### Running the Code

1. **Set Camera Parameters**: Update the `PinholeCamera` instance in `test.py` with your camera's parameters:

    ```python
    cam = PinholeCamera(1241.0, 376.0, 718.8560, 718.8560, 607.1928, 185.2157)
    ```

2. **Load Ground Truth Data**: Specify the path to the ground truth annotations file in the `VisualOdometry` class:

    ```python
    vo = VisualOdometry(cam, '/path/to/your/annotations.txt')
    ```

3. **Load Image Sequence**: Specify the path to the image sequence:

    ```python
    img_path = '/path/to/your/images/' + str(img_id).zfill(6) + '.png'
    ```

4. **Run the Script**:

    ```bash
    python test.py
    ```

### Outputs

- **Trajectory Visualization**: The script displays two windows: 
  - One showing the current frame being processed.
  - Another showing the estimated trajectory (green) compared to the ground truth (red).
- **Saved Map**: The trajectory visualization is saved as `map.png`.

## Code Overview

### `test.py`

The main script performs the following steps:

1. **Initialize Camera**: Create an instance of `PinholeCamera`.
2. **Initialize Visual Odometry**: Create an instance of `VisualOdometry`.
3. **Image Loop**:
   - Load each image frame.
   - Update visual odometry using `vo.update`.
   - Plot the estimated trajectory.

### `visual_odometry.py`

This file contains the core implementation for visual odometry.

1. **`PinholeCamera` Class**:
   - Stores camera parameters and distortion coefficients.

2. **`VisualOdometry` Class**:
   - Processes frames and estimates the camera's motion.
   - **Key Methods**:
     - `processFirstFrame`: Detects features in the first frame.
     - `processSecondFrame`: Estimates motion between the first and second frames.
     - `processFrame`: Updates motion estimation for subsequent frames.
     - `update`: Main function to process each new frame.

3. **`featureTracking` Function**:
   - Tracks features between two frames using Lucas-Kanade optical flow.

## Python 3 Optimization

This project was originally designed for Python 2. The following changes were made to ensure Python 3 compatibility:

- Updated `print` statements to Python 3 syntax.
- Ensured `numpy` and `OpenCV` functions work with Python 3.
- Adjusted data types and array handling to match Python 3 requirements.

## Reference

This project is adapted from the original implementation by [uoip/monoVO-python](https://github.com/uoip/monoVO-python).

## License

This project is released under the MIT License.
