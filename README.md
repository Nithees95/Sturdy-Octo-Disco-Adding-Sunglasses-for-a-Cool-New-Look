# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

##program:
```
DEVELOPED BY : NITHEESH YEGAVINTI
REG NO: 212224040370

```

##Import libraries

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

##Load the Face Image

faceImage = cv2.imread('/content/DSC_5426.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="533" height="535" alt="image" src="https://github.com/user-attachments/assets/1d4f5ab0-ecc3-4566-9e4b-6a0a7d693da7" />

```
faceImage.shape

```
<img width="222" height="45" alt="image" src="https://github.com/user-attachments/assets/faa37965-4ad2-4156-a4e6-fb209808df71" />

```

glassJPG = cv2.imread('sunglass')
plt.imshow(glassJPG[:,:,::-1]); plt.title("sunglass")
print("Glass shape:", glassJPG.shape)
```
<img width="729" height="440" alt="image" src="https://github.com/user-attachments/assets/df4fc031-5b7a-488b-b4cb-6e3b4477a1b4" />

```
#Show generated mask
plt.subplot(122)
plt.imshow(glassMask1, cmap='gray_r')
plt.title('Sunglass Mask (generated)')
```
<img width="1010" height="314" alt="image" src="https://github.com/user-attachments/assets/1a3e5f31-16a0-417c-afb6-85fafa8d73b6" />

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
#Load images
faceImage = cv2.imread('/content/DSC_5426.jpg')
glassJPG = cv2.imread('/content/kkk.jpg')

#Check if images loaded correctly
if faceImage is None or glassJPG is None:
    print("Error: Check your file paths!")
else:
    face_h, face_w, _ = faceImage.shape

    #Resize glasses to ~50% of face width
    new_w = int(face_w * 0.4)
    new_h = int(new_w * glassJPG.shape[0] / glassJPG.shape[1])
    glass_resized = cv2.resize(glassJPG, (new_w, new_h))

    #Create mask
    glass_gray = cv2.cvtColor(glass_resized, cv2.COLOR_BGR2GRAY)
    _, mask = cv2.threshold(glass_gray, 246, 260, cv2.THRESH_BINARY_INV)
    mask_inv = cv2.bitwise_not(mask)

    # Adjusted position to place glasses on eyes
    x = int(face_w * 0.30)   # x offset (centered)
    y = int(face_h * 0.24)   # y offset (move up from nose to eyes)

    #ROI on face
    roi = faceImage[y:y+new_h, x:x+new_w]

    if roi.shape[0] > 0 and roi.shape[1] > 0:
        bg = cv2.bitwise_and(roi, roi, mask=mask_inv)
        fg = cv2.bitwise_and(glass_resized, glass_resized, mask=mask)
        combined = cv2.add(bg, fg)
        faceImage[y:y+new_h, x:x+new_w] = combined

    #Show result
    plt.figure(figsize=[10,10])
    plt.imshow(cv2.cvtColor(faceImage, cv2.COLOR_BGR2RGB))
    plt.title("Face with Sunglasses")
    plt.axis("off")
    plt.show()
 ``` 
<img width="755" height="834" alt="image" src="https://github.com/user-attachments/assets/be809ec7-9a03-4bda-a2d0-7fbc6149086e" />


