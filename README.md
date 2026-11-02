# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
# NAME: N.KANISHKA
# REG NO: 212225230127

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

## Program:
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread('kanish1.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
faceImage.shape
glassPNG = cv2.imread('Sunglasss.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
glassPNG = cv2.resize(glassPNG,(220, 65))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
cyan_bg = (glassBGR[:, :, 0] > 150) & (glassBGR[:, :, 1] > 150) & (glassBGR[:, :, 2] < 120)
glassMask1 = np.where(cyan_bg, 0, 255).astype(np.uint8)
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[185:250, 145:365]=glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask/255)
faceWithGlassesArithmetic = faceImage.copy()
eyeROI= faceWithGlassesArithmetic[185:250, 145:365]
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))
maskedGlass = cv2.multiply(glassBGR,glassMask)
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
faceWithGlassesArithmetic[185:250, 145:365]=eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");

```

## Output:

<img width="467" height="567" alt="image" src="https://github.com/user-attachments/assets/25a2b792-964a-4e1e-a507-f06d843cc18a" />
<img width="717" height="378" alt="image" src="https://github.com/user-attachments/assets/42e6e0fb-6951-4a6e-91e4-f3b58fe0500c" />
<img width="1363" height="237" alt="image" src="https://github.com/user-attachments/assets/caa4448a-13b9-4233-9eb3-fa76116bf5a0" />
<img width="432" height="546" alt="image" src="https://github.com/user-attachments/assets/176ceb66-adab-4ff2-81a9-506d0b590602" />
<img width="1365" height="197" alt="image" src="https://github.com/user-attachments/assets/2fd0a7d4-2889-48cc-b5fb-5436f243add4" />
<img width="1385" height="780" alt="image" src="https://github.com/user-attachments/assets/188b5e92-3314-4cc2-92e8-545d8a8c06d8" />

## Result: 
The project successfully detected the face in the input image and added sunglasses automatically using OpenCV. The output image showed the sunglasses correctly positioned on the face, demonstrating the effectiveness of basic image processing techniques.
