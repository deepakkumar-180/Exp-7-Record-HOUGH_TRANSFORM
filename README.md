# EXP-7 Lane Detection
# NAME:DEEPAKKUMAR S
# REG NO : 212225230042
##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

##  Algorithm & Explanation

---

###  Step 1: Import Libraries

```

import cv2
import numpy as np
import matplotlib.pyplot as plt

```
---

###  Step 2: Read the Image

```
img = cv2.imread('road1.png')

if img is None:
    print("Image not found")
    exit()
```
---
###  Step 3: Convert to Grayscale

```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

```

---

###  Step 4: Display Images

```
plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(gray, cmap='gray')
plt.title("Grayscale Image")
plt.axis("off")

plt.show()

```

---

###  Step 5: Thresholding

```
threshold = cv2.threshold(
    gray, 150, 255, cv2.THRESH_BINARY
)[1]

plt.imshow(threshold, cmap='gray')
plt.title("Thresholded Image")
plt.axis("off")
plt.show()

```
---

###  Step 6: Region of Interest (ROI)

```
height, width = gray.shape

mask = np.zeros_like(gray)

polygon = np.array([[
    (0, height),
    (width, height),
    (width, int(height * 0.6)),
    (0, int(height * 0.6))
]], np.int32)

cv2.fillPoly(mask, polygon, 255)

roi = cv2.bitwise_and(threshold, mask)

plt.imshow(roi, cmap='gray')
plt.title("ROI Masked Image")
plt.axis("off")
plt.show()

```

---

### Step 7: Edge Detection (Canny)

```
edges = cv2.Canny(roi, 50, 150)

plt.imshow(edges, cmap='gray')
plt.title("Edge Detected Image")
plt.axis("off")
plt.show()

```


---

###  Step 8: Gaussian Blur

```
blur = cv2.GaussianBlur(edges, (5,5), 0)

plt.imshow(blur, cmap='gray')
plt.title("Smoothed Image")
plt.axis("off")
plt.show()

```
---

###  Step 9: Hough Transform

```
lines = cv2.HoughLinesP(
    blur,
    1,
    np.pi/180,
    50,
    minLineLength=50,
    maxLineGap=100
)

line_image = img.copy()

if lines is not None:
    lines = np.array(lines).reshape(-1, 4)

    for x1, y1, x2, y2 in lines:
        cv2.line(
            line_image,
            (int(x1), int(y1)),
            (int(x2), int(y2)),
            (0, 255, 0),
            3
        )

plt.imshow(cv2.cvtColor(line_image, cv2.COLOR_BGR2RGB))
plt.title("Detected Lane Lines")
plt.axis("off")
plt.show()

```

---

### Step 10: Lane Detection Logic

```
plt.figure(figsize=(10,5))
plt.imshow(cv2.cvtColor(line_image, cv2.COLOR_BGR2RGB))
plt.title("Final Lane Detection")
plt.axis("off")
plt.show()

```
---

##  Expected Output

* Original image
* Grayscale image
* Thresholded image
* ROI masked image
* Edge detected image
* Smoothed image
* Detected lines
* Final lane detection output

---
## OUTPUT
<img width="794" height="240" alt="download" src="https://github.com/user-attachments/assets/fc937c5a-0637-4d19-8fc0-8df4cc9ef41d" />
<img width="515" height="320" alt="download" src="https://github.com/user-attachments/assets/ab7d666b-52cf-4451-88c3-e442903c6a87" />
<img width="515" height="320" alt="download" src="https://github.com/user-attachments/assets/2a41c51f-6d63-4cd6-9366-27bb6472b996" />
<img width="515" height="320" alt="download" src="https://github.com/user-attachments/assets/372d78be-4fc8-4faf-9cdb-0b73e3088e7f" />
<img width="515" height="320" alt="download" src="https://github.com/user-attachments/assets/103cfa65-fe4c-46c4-ad83-543e81e9245c" />
<img width="515" height="320" alt="download" src="https://github.com/user-attachments/assets/c69db262-d044-4280-81ab-eb9fe7f1fb2a" />
<img width="705" height="427" alt="download" src="https://github.com/user-attachments/assets/2ce8a968-531e-449b-a71e-12b58c1123fd" />





##  Instructions

* Fill ONLY in `# Your Code Here` sections
* Do NOT change existing code
* Run step-by-step
* Verify outputs

---

## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---
