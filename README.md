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
##PROGRAM AND OUTPUT:

```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the Face Image
import cv2
import matplotlib.pyplot as plt
faceImage = cv2.imread('face.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")

```

<img width="327" height="435" alt="download" src="https://github.com/user-attachments/assets/ad1dba85-7c43-486b-ab24-9d505cbffadd" />

```
faceImage.shape
faceImage.shape
```


(1599, 1137, 3)

```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```

<img width="560" height="285" alt="download" src="https://github.com/user-attachments/assets/8e83f160-ff22-4535-8a25-c4815249d7b4" />

```

# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(550,200))
print("sunglass.png".format(glassPNG.shape))

# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');

```

<img width="1218" height="258" alt="download" src="https://github.com/user-attachments/assets/b537bf58-da64-431e-8c6d-9fc3cb841758" />

```

# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[440:640,310:860]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```

<img width="327" height="418" alt="download" src="https://github.com/user-attachments/assets/7bca9f81-e664-484b-aac5-9c7fa73b48df" />

```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[440:640,310:860]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```

<img width="1606" height="231" alt="download" src="https://github.com/user-attachments/assets/db2d00a6-7774-4e00-b817-adca6182d7cb" />

```

# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[440:640,310:860]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

<img width="1614" height="1056" alt="download" src="https://github.com/user-attachments/assets/8789520a-d483-4492-b51f-2a392da9bee9" />

##result:
thus the experiment is executed sucess
