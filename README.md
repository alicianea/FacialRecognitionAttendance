# Facial Recognition Attendance System

A python program that uses your webcam to recognize faces in real time and automatically log attendance to a CSV file. Known people are outlined in green with their name, and unrecognized faces are outlined in red and labeled "Unknown".

# Features

* Real-time face detection and recognition from a webcam feed
* Automatic attendance logging (name + time) to Attendance.csv
* Each person is logged only once per session, so there are no duplicate entries
* Add new people/faces by dropping a photo (.jpg) into the Images folder
* Visual feedback: green box + name for recognized faces, red box for unknown faces.
* Shows a placeholder image (`unknown.jpg`) beneath unrecognized faces

# How it works

- The program loads every image in the Images folder. The filename becomes the person's name.
- Each image is converted into a 128-dimension face encoding using the face_recognition library.
- The webcam feed is captured frame by frame. Each frame is shrunk to 25% of its size to speed up processing.
- Faces in the frame are detected and encoded, then compared against the known encodings.
- If a match is found, the person's name is drawn on screen and their name and check-in time are written to Attendance.csv (if they aren't already listed).
- If no match is found, the face is marked "Unknown" and unknown.jpg is displayed below it. This is optional to have, the program runs fine without it.

# Requirements

* Python 3.7+
* A working webcam
* The following libraries:
    * opencv-python
    * numpy
    * face_recognition (dlib)
 
To install the necessary dependencies:

`pip install opencv-python numpy`

`pip install cmake`

`pip install dlib`

`pip install face_recognition`

Note: `dlib` requires CMake and a C++ compiler to build. On Windows, install Visual Studio Build Tools with "Desktop development with C++" workload. On macOS, run `brew install cmake`.

# Project Structure

.

├── main.py             # The main program (rename to match your file)

├── Images/             # Photos of known people (one per person)

│   ├── Alice.jpg

│   └── Bob.jpg

├── Attendance.csv      # Attendance log (must exist before first run)

└── unknown.jpg         # Image shown beneath unrecognized faces

# Setup

Add known faces. Place one clear, front-facing photo of each person in the Images folder. Name each file after the person, for example `Alice.jpg` becomes "ALICE".

Create the attendance file. One has already been provided, but if another one is necessary, name the file `Attendance.csv` in the project folder. A header row is recommended: `Name,Time`

Add an unknown-face image (optional). Place an image named `unknown.jpg` in the project folder to be displayed below any face that isn't recognized. 

# Usage

To run the program:

`python main.py`

The webcam will open. Position yourself in front of the camera, and once you're recognized, your name and check-in time are saved to Attendance.csv.

To stop the program, click on the terminal and type: `Ctrl + C`

# Limitations

* Time only, no dates are recorded. Attendance is only logged once per name in the file, so a new `Attendance.csv` or clearing the current one is necessary for a new day.
* No quit key. The program has no built-in exit key, so the program is stopped with `Ctrl + C` in the terminal.
* If the image in `Images` contains no detectable face, it is skipped during encoding, so make sure every reference image contains a clear face.
* Recognition can be affected by lighting, camera angle, and image quality. It should not be relied on as a sole security or verification measure.



