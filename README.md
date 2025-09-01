Camera Calibration with OpenCV in Google Colab

This project focuses on performing camera calibration using OpenCV within the Google Colab environment, where a webcam is connected through a JavaScript–Python bridge. Camera calibration is an essential step in computer vision, as it allows us to correct lens distortions and determine intrinsic camera parameters such as the focal length, optical center, and distortion coefficients. These parameters are critical in tasks like 3D reconstruction, robotics, augmented reality, and image processing.

Step 1: Webcam Setup in Google Colab

Since Google Colab runs in a browser environment without direct access to local devices, a JavaScript function is used to connect to the system’s webcam. This function streams video, captures a frame, and encodes it into a format that Python can read. Using a Python bridge, the captured frame is transferred into a NumPy array so that it can be processed by OpenCV.

Step 2: Chessboard Configuration

A chessboard pattern is used as the calibration target because it provides well-defined, easily detectable corner points. The inner corners of the chessboard grid are specified (for example, 9×6 corners), along with the real-world size of each square (in millimeters). With this information, a 3D reference of the chessboard is created in object coordinates, representing the ideal geometry of the pattern. This acts as the "ground truth" against which the camera’s projection is compared.

Step 3: Image Capture for Calibration

The calibration requires multiple images of the chessboard pattern taken from different angles and positions. The program captures images in a loop (12 in this project) and automatically attempts to detect the chessboard corners in each frame using cv2.findChessboardCorners. If the corners are detected successfully, they are refined to sub-pixel accuracy with cv2.cornerSubPix, stored along with their corresponding 3D points, and visualized by overlaying the detected corners on the captured frame. If the chessboard is not detected, the user is prompted to adjust the position, orientation, or lighting before another capture.

Step 4: Camera Calibration

After a sufficient number of valid chessboard images are collected, OpenCV’s cv2.calibrateCamera function is applied. This function compares the known 3D coordinates of the chessboard points with their detected 2D positions in the images. From this, it estimates the camera’s intrinsic parameters (focal lengths and optical center), distortion coefficients (radial and tangential lens distortions), and extrinsic parameters (rotation and translation vectors for each image).

Step 5: Output of Calibration Results

The results are displayed clearly at the end of the process:

Camera Matrix – Describes intrinsic camera parameters.

Distortion Coefficients – Capture the effects of lens distortion.

Focal Lengths (fx, fy) – Indicate how strongly the camera lens projects the scene onto the sensor.

Optical Center (cx, cy) – The principal point on the image plane where the optical axis intersects.

These parameters can later be used to undistort images, improve the accuracy of computer vision pipelines, or integrate the camera into augmented reality and robotics systems.

Applications of This Project

Image Undistortion – Correcting distorted images to make straight lines appear straight.

3D Reconstruction – Essential for mapping and structure-from-motion projects.

Augmented Reality (AR) – Overlaying virtual objects in the real world with geometric accuracy.

Robotics and Navigation – Allowing robots to perceive the environment more accurately.
