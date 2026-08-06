# WORKSHOP – 1

# Sturdy Octo Disco – Sunglass Overlay using OpenCV

Welcome to **Sturdy Octo Disco**, a fun and creative Digital Image Processing project that overlays stylish sunglasses onto a passport-size photo using image processing techniques. This project demonstrates image masking, alpha blending, and image manipulation using Python and OpenCV.

---

## Features

- Detects and processes the face image.
- Overlays transparent sunglasses on the eye region.
- Uses alpha channel masking for realistic blending.
- Works with passport-size photographs.
- Easy to customize with different sunglasses.

---

## Technologies Used

- Python
- OpenCV
- NumPy
- Matplotlib

---

# Program & Output

### NAME
**SABARISH A**

### REG. NO.
**212225230232**

---

## Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

## Load the Face Image

```python
faceImage = cv2.imread('myimage.jpeg')
plt.imshow(faceImage[:,:,::-1])
plt.title("Face Image")
```

### Output

<img width="339" height="486" alt="image" src="https://github.com/user-attachments/assets/5f4b4dda-cc90-4834-bdc0-406404bc2297" />


---

## Display Image Size

```python
faceImage.shape
```

### Output

<img width="128" height="43" alt="image" src="https://github.com/user-attachments/assets/ae08a510-9496-46c5-a01f-1b8f0be54434" />


---

## Load Sunglass Image with Alpha Channel

```python
glassPNG = cv2.imread('sunglass.png', -1)
plt.imshow(glassPNG[:,:,::-1])
plt.title("Sunglass Image")
```

### Output

<img width="649" height="342" alt="image" src="https://github.com/user-attachments/assets/baf858ec-8655-42b7-ab30-2169925f73a4" />


---

## Resize Sunglass Image

```python
glassPNG = cv2.resize(glassPNG, (275,118))
print(glassPNG.shape)
```

### Output

<img width="252" height="46" alt="image" src="https://github.com/user-attachments/assets/f2041059-0dea-4950-9a51-3ecf4a9e3aae" />


---

## Separate RGB and Alpha Channels

```python
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```

---

## Display RGB and Alpha Channel

```python
plt.figure(figsize=(15,6))

plt.subplot(121)
plt.imshow(glassBGR[:,:,::-1])
plt.title("Sunglass RGB")

plt.subplot(122)
plt.imshow(glassMask1,cmap="gray")
plt.title("Alpha Mask")
```

### Output

<img width="831" height="153" alt="image" src="https://github.com/user-attachments/assets/968fc277-9788-4fbd-beb4-b3f6caced320" />


---

## Naive Overlay Method

```python
glassBGR = cv2.resize(glassBGR,(275,118))

faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[508:626,248:523] = glassBGR

plt.imshow(faceWithGlassesNaive[:,:,::-1])
```

### Output

<img width="394" height="489" alt="image" src="https://github.com/user-attachments/assets/77a3f84e-8d8b-4a2c-924c-fb3eb688f5f1" />


---

## Alpha Blending using Mask

```python
glassBGR = cv2.resize(glassBGR,(275,118))
glassMask1 = cv2.resize(glassMask1,(275,118))

glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask/255)

faceWithGlassesArithmetic = faceImage.copy()

eyeROI = faceWithGlassesArithmetic[508:626,248:523]

maskedEye = cv2.multiply(eyeROI,(1-glassMask))

maskedGlass = cv2.multiply(glassBGR,glassMask)

eyeRoiFinal = cv2.add(maskedEye,maskedGlass)

faceWithGlassesArithmetic[508:626,248:523] = eyeRoiFinal

plt.figure(figsize=(20,20))

plt.subplot(131)
plt.imshow(maskedEye[:,:,::-1])
plt.title("Masked Eye Region")

plt.subplot(132)
plt.imshow(maskedGlass[:,:,::-1])
plt.title("Masked Sunglass Region")

plt.subplot(133)
plt.imshow(faceWithGlassesArithmetic[:,:,::-1])
plt.title("Final Augmented Image")

plt.show()
```

### Output

<img width="827" height="466" alt="image" src="https://github.com/user-attachments/assets/fbccb193-bd57-4d76-9a9d-e1be0c05b709" />


---

## Final Output

```python
plt.figure(figsize=(15,8))

plt.subplot(121)
plt.imshow(faceImage[:,:,::-1])
plt.title("Original Image")

plt.subplot(122)
plt.imshow(faceWithGlassesArithmetic[:,:,::-1])
plt.title("Image with Sunglasses")

plt.show()
```

### Output

<img width="824" height="682" alt="image" src="https://github.com/user-attachments/assets/8b6827fc-8e75-43d4-ada9-2aaaee39493f" />


---

# Result

Thus, the **Sturdy Octo Disco** workshop was completed successfully by overlaying a transparent sunglass image onto the face image using OpenCV image processing techniques. The project successfully demonstrates image masking, alpha blending, and region-of-interest (ROI) manipulation to achieve a realistic sunglass overlay.
