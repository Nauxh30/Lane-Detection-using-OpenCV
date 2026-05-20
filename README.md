# Lane Detection using OpenCV 🚗🛣️

## Overview

This project demonstrates **Lane Detection** using Python and OpenCV.  
The system detects road lane markings from an image using:

- Grayscale Conversion
- Gaussian Blur
- Canny Edge Detection
- Region of Interest Masking
- Hough Line Transform

The detected lane lines are highlighted on the original road image.

---

# Objectives

- Detect road lane markings from an input image
- Apply image preprocessing techniques
- Use Hough Transform for line detection
- Visualize detected lanes

---

# Technologies Used

- Python 3
- OpenCV
- NumPy
- Matplotlib

---

# Required Libraries

Install dependencies using:

```bash
pip install opencv-python numpy matplotlib
```

---

# Project Workflow

1. Read input image
2. Convert image to grayscale
3. Apply Gaussian Blur
4. Detect edges using Canny Edge Detection
5. Define Region of Interest (ROI)
6. Apply Hough Line Transform
7. Draw detected lane lines
8. Display final output

---

# Program

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read image
img = cv2.imread("lan_img1.jpg")

# Convert BGR to RGB
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Convert to grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Apply Gaussian Blur
blur = cv2.GaussianBlur(gray, (5, 5), 0)

# Perform Canny Edge Detection
edges = cv2.Canny(blur, 50, 150)

# Define Region of Interest
height = edges.shape[0]
polygons = np.array([
    [(200, height), (1100, height), (550, 250)]
])

mask = np.zeros_like(edges)
cv2.fillPoly(mask, polygons, 255)

masked_image = cv2.bitwise_and(edges, mask)

# Hough Line Transform
lines = cv2.HoughLinesP(
    masked_image,
    2,
    np.pi / 180,
    threshold=100,
    minLineLength=40,
    maxLineGap=5
)

# Function to draw lines
def draw_lines(image, lines):
    if lines is not None:
        for line in lines:
            x1, y1, x2, y2 = line[0]
            cv2.line(image, (x1, y1), (x2, y2), (0, 255, 0), 5)

# Create blank image
line_image = np.zeros_like(img)

# Draw lane lines
draw_lines(line_image, lines)

# Combine images
combo_image = cv2.addWeighted(img_rgb, 0.8, line_image, 1, 1)

# Display output
plt.figure(figsize=(15, 10))
plt.imshow(combo_image)
plt.title("Lane Detection Output")
plt.axis("off")
plt.show()
```

---

# Output

- Original road image
- Edge-detected image
- Final lane-detected image with highlighted lanes

---

# Result

Thus, lane detection was successfully implemented using OpenCV and Python.

The system accurately identifies lane markings from the road image using image processing techniques and Hough Line Transform.

---

# Applications

- Self-driving cars
- Driver assistance systems
- Road safety monitoring
- Autonomous navigation

---

# Conclusion

This project demonstrates how computer vision techniques can be used to detect lanes effectively from road images. Lane detection is a fundamental component in autonomous vehicle systems and smart transportation technologies.

🚘 Pixels found the road. Humanity survives another curve.
