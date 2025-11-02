# 🎯 Static Motion Detection Within Region of Interest (ROI)

This project demonstrates **real-time motion detection** using **Python** and **OpenCV**.
It continuously captures frames from a webcam, compares differences between consecutive frames, and detects motion **within a specific Region of Interest (ROI)**.

---

## 🧠 Project Overview

The program focuses on detecting **motion only in a selected area** of the frame, ignoring unnecessary background movement.
It highlights the ROI using a green rectangle and displays “Motion Detected” when significant motion is found.

---

## 🎥 Demo Video

▶️ **[Watch on YouTube]()**

---

## 👩‍💻 Author

**Bhavana Shamanthula**
🔗 [LinkedIn Profile](www.linkedin.com/in/shamanthula-bhavana-7343bb331)
🔗 [GitHub Repository](https://github.com/Shamanthula-Bhavana05/Static-Motion-Detection-Using-Python-and-OpenCV)

---

## 🧩 Technologies Used

* **Python 3.x**
* **OpenCV (cv2)**
* **NumPy**

---

## ⚙️ Installation & Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/your-username/Static-Motion-Detection-Using-Python-and-OpenCV.git
   cd Static-Motion-Detection-Using-Python-and-OpenCV
   ```

2. **Install dependencies**

   ```bash
   pip install opencv-python numpy
   ```

3. **Run the program**

   ```bash
   python motion_detection.py
   ```

4. **Press 'q' or 'Q' to exit.**

---

## 💻 Code Explanation

```python
import cv2
import numpy as np

# Start capturing video
vid = cv2.VideoCapture(0)

# Get first frame
succ1, frame1 = vid.read()
cv2.namedWindow('MOTION DETECTION PROJECT', cv2.WINDOW_FREERATIO)

if not succ1:
    print('Failed to capture')
    exit()

# Convert first frame to grayscale
framegray1 = cv2.cvtColor(frame1, cv2.COLOR_BGR2GRAY)

# Define coordinates for cropping (ROI)
x1, x2, y1, y2 = 30, 200, 200, 400

while True:
    succ, frame = vid.read()
    if not succ:
        break

    # Convert current frame to grayscale
    framegray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # Crop both frames to ROI
    roi1 = framegray1[y1:y2, x1:x2]
    roi2 = framegray[y1:y2, x1:x2]

    # Subtract frames to detect motion
    diff = cv2.subtract(roi1, roi2) / 255

    # Draw ROI rectangle
    cv2.rectangle(frame, (x1, y1), (x2, y2), (0, 255, 0), 2)

    # Motion detection threshold
    if np.sum(diff) > 500:
        cv2.putText(frame, 'Motion Detected', (100, 100),
                    cv2.FONT_HERSHEY_SIMPLEX, 2, (0, 0, 255), 2)

    cv2.imshow('MOTION DETECTION PROJECT', frame)

    # Exit on key press 'q' or 'Q'
    if cv2.waitKey(1) in [ord('q'), ord('Q')]:
        break

    # Update previous frame
    framegray1 = framegray

cv2.destroyAllWindows()
```

---

## 🖼️ Output Example

✅ A green box marks the ROI.
⚠️ When motion occurs inside the box, red text “Motion Detected” appears on screen.

---

## 💡 Applications

* Surveillance systems
* Smart home monitoring
* Motion-based automation
* Security camera alerts

