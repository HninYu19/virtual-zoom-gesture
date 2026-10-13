Virtual Zoom Gesture Control with OpenCV

A Python program that lets you zoom a picture with your hands in front of a webcam. It tracks both hands in real time. When you show a thumb-and-index-finger gesture with each hand and move the hands apart or together, the image on the screen gets bigger or smaller.

Features
Real-time two-hand tracking from the webcam (1280 x 720)
Gesture check: both hands must show thumb and index finger up (an "L" shape), with the other fingers folded
The distance between the two hands controls the zoom
The image stays centered between your hands while you zoom
Hand landmarks are drawn on the video so you can see what is being tracked
How It Works
Capture video: OpenCV reads frames from the webcam.
Detect hands: HandDetector from the cvzone library (built on MediaPipe hand tracking) finds up to two hands with a detection confidence of 0.8.
Check the gesture: fingersUp() returns which fingers are raised for each hand. The zoom starts only when both hands return [1, 1, 0, 0, 0] (thumb and index finger up).
Measure the distance: the program stores the starting distance between the two hand centers. While the gesture is held, it measures the current distance again.
Compute the scale: the change from the starting distance, divided by 2, is added to the image size. Hands further apart make the image larger, and hands closer together make it smaller.
Draw the image: scenery.jpg is resized with cv2.resize and pasted onto the video frame, centered between the two hands.
When the gesture stops or a hand leaves the frame, the starting distance is reset.
Project Structure
virtual-zoom-gesture/
├── main.py        # Hand tracking and zoom code
└── scenery.jpg    # The image that is zoomed (you can replace it)
Requirements
Python 3.10 or newer
A webcam
Python packages:
pip install opencv-python cvzone mediapipe
Setup and Usage
Clone this repository.
Install the packages above.
Keep scenery.jpg in the same folder as main.py, or replace it with your own picture (keep the file name, or change it in the code).
Run the program from inside the project folder:
python main.py
Show both hands to the camera with thumb and index finger raised on each hand.
Move your hands apart to zoom in, and together to zoom out.
To stop the program, click the terminal and press Ctrl + C.
Limitations
Good lighting and a clear view of both hands are needed. Tracking can fail in dim light.
The zoom works only while both hands show the exact gesture.
If the image grows beyond the video frame, it is not drawn until it fits again.
The program has no quit key inside the video window yet.
The zoom scale is not limited, so the image can become very small or very large.
Ideas for Improvement
Add a quit key (for example, press q) inside the video window
Set a minimum and maximum zoom level
Smooth the zoom so it does not jump between frames
Let the user choose the image from the command line
Add more gestures, such as swiping to move to the next picture
Technologies

Python, OpenCV, cvzone, MediaPipe hand tracking

Credits

Hand tracking is provided by the cvzone library and Google's MediaPipe.
