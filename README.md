# Webcam Face Detection with OpenCV

This project demonstrates real-time face detection using your webcam and OpenCV's Haar Cascade classifier.

## Features

- Captures live video feed from your webcam.
- Detects human faces in real-time using the Haar Cascade classifier.
- Draws rectangles around detected faces.
- Exits cleanly on pressing the `q` key.

## Requirements

- Python 3.x
- OpenCV (`opencv-python` package)

## Installation

1. **Clone the Repository** (if applicable):
    ```bash
    git clone https://github.com/yourusername/your-repo-name.git
    cd your-repo-name
    ```

2. **Install Dependencies**:
    ```bash
    pip install opencv-python
    ```

## Usage

1. Save the provided Python code to a file, e.g., `face_detection.py`.
2. Run the script:
    ```bash
    python face_detection.py
    ```
3. A window will open displaying your webcam feed with rectangles around detected faces.
4. Press the `q` key to exit the application.

## Code Explanation

```python
import cv2

# Load the Haar Cascade classifier for face detection
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')

# Start capturing video from the webcam
cap = cv2.VideoCapture(0)
if not cap.isOpened():
    print("Error: Could not open the webcam")
    exit()

while True:
    ret, frame = cap.read()
    if not ret:
        print("Failed to grab frame")
        break

    # Convert the frame to grayscale for face detection
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # Detect faces in the grayscale frame
    faces = face_cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5)

    # Draw rectangles around detected faces
    for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)

    # Display the frame with detected faces
    cv2.imshow('Webcam Live Feed', frame)

    # Break the loop if 'q' is pressed
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Release resources
cap.release()
cv2.destroyAllWindows()
```

## Troubleshooting

- If the webcam cannot be opened, ensure it is connected and not used by another application.
- On some systems, you may need to change the camera index from `0` to `1` or higher in `cv2.VideoCapture(0)`.

## License

This project is licensed under the MIT License.
