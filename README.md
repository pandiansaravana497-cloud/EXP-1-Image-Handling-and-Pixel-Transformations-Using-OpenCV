# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** PON SARAVANA PANDIAN B
- **Register Number:** 212225230207

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
img_gray = cv2.imread(eagle_path, cv2.IMREAD_GRAYSCALE)

if img_gray is None:
    raise FileNotFoundError("Eagle_in_Flight.jpg not found. Check the path.")

print("Image loaded successfully!")
```

#### 2. Print the image width, height & Channel.
```python
height, width = img_gray.shape
channels = 1

print("Width:", width)
print("Height:", height)
print("Channel:", channels)
```

#### 3. Display the image using matplotlib imshow().
```python
plt.figure(figsize=(8, 6))
plt.imshow(img_gray, cmap="gray")
plt.title("Eagle Image - Grayscale")
plt.axis("off")
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite(os.path.join(base, "Eagle_Grayscale.png"), img_gray)
print("Grayscale image saved successfully!")
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
saved_gray = cv2.imread(
    os.path.join(base, "Eagle_Grayscale.png"),
    cv2.IMREAD_GRAYSCALE
)

img_color = cv2.cvtColor(saved_gray, cv2.COLOR_GRAY2BGR)
img_color_rgb = cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
height, width, channels = img_color.shape

print("Width:", width)
print("Height:", height)
print("Channels:", channels)

plt.imshow(img_color_rgb)
plt.title("Eagle Image - Three Channels")
plt.axis("off")
plt.show()
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
# Display image to identify crop coordinates
plt.figure(figsize=(10, 6))
plt.imshow(img_color_rgb)
plt.title("Identify Eagle Crop Coordinates")
plt.axis("on")
plt.show()
```

#### 8. Resize the image up by a factor of 2x.
```python
eagle_resized = cv2.resize(
    eagle_crop,
    None,
    fx=2,
    fy=2,
    interpolation=cv2.INTER_LINEAR
)

plt.imshow(cv2.cvtColor(eagle_resized, cv2.COLOR_BGR2RGB))
plt.title("Eagle Resized by 2x")
plt.axis("off")
plt.show()
```

#### 9. Flip the cropped/resized image horizontally.
```python
eagle_flipped = cv2.flip(eagle_resized, 1)

plt.imshow(cv2.cvtColor(eagle_flipped, cv2.COLOR_BGR2RGB))
plt.title("Horizontally Flipped Eagle")
plt.axis("off")
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
apollo = cv2.imread(apollo_path)

if apollo is None:
    raise FileNotFoundError("Apollo-11-launch.jpg not found. Check the path.")

apollo_rgb = cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(9, 6))
plt.imshow(apollo_rgb)
plt.title("Apollo 11 Launch - Original")
plt.axis("off")
plt.show()

print("Image dimensions:", apollo.shape)
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = "Apollo 11 Saturn V Launch, July 16, 1969"
font_face = cv2.FONT_HERSHEY_PLAIN

h, w = apollo.shape[:2]
font_scale = max(1, w / 1000)
thickness = 2

text_size = cv2.getTextSize(
    text, font_face, font_scale, thickness
)[0]

text_x = (w - text_size[0]) // 2
text_y = h - 20

cv2.putText(
    apollo, text, (text_x, text_y),
    font_face, font_scale, (255, 255, 255),
    thickness, cv2.LINE_AA
)
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
# Example coordinates; change them to fit your image
x1, y1 = 100, 50
x2, y2 = apollo.shape[1] - 100, apollo.shape[0] - 50

magenta = (255, 0, 255)  # BGR format

cv2.rectangle(
    apollo, (x1, y1), (x2, y2),
    magenta, 3
)
```

#### 13. Display the final annotated image.
```python
apollo_final_rgb = cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 7))
plt.imshow(apollo_final_rgb)
plt.title("Apollo 11 Launch - Annotated Image")
plt.axis("off")
plt.show()

cv2.imwrite(os.path.join(base, "Apollo_Annotated.jpg"), apollo)
```

#### 14. Read the image ('Boy.jpg').
```python
img = cv2.imread(boy_path)

if img is None:
    raise FileNotFoundError("boy.jpg not found. Check the path.")

img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.imshow(img_rgb)
plt.title("Original Boy Image")
plt.axis("off")
plt.show()
```

#### 15. Adjust the brightness of the image.
```python
# Create a matrix of ones with float64 data type
matrix_ones = np.ones(img.shape, dtype=np.float64)

# Convert to the image's data type for OpenCV arithmetic
matrix = matrix_ones.astype(img.dtype)

img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)
```

#### 16. Create brighter and darker images.
```python
# Create a matrix of ones with float64 data type
matrix_ones = np.ones(img.shape, dtype=np.float64)

# Convert to the image's data type for OpenCV arithmetic
matrix = matrix_ones.astype(img.dtype)

img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
images = [img, img_darker, img_brighter]
titles = ["Original Image", "Darker Image", "Brighter Image"]

plt.figure(figsize=(15, 5))

for i in range(3):
    plt.subplot(1, 3, i + 1)
    plt.imshow(cv2.cvtColor(images[i], cv2.COLOR_BGR2RGB))
    plt.title(titles[i])
    plt.axis("off")

plt.tight_layout()
plt.show()
```

#### 18. Modify the image contrast.
```python
# Lower contrast
matrix_low = np.ones(img.shape, dtype=np.float64) * 0.8
img_lower = (img.astype(np.float64) * matrix_low).astype(np.uint8)

# Higher contrast using factors 1.1 and 1.2
matrix1 = np.ones(img.shape, dtype=np.float64) * 1.1
matrix2 = np.ones(img.shape, dtype=np.float64) * 1.2

img_higher1 = (img.astype(np.float64) * matrix1).astype(np.uint8)
img_higher2 = (img.astype(np.float64) * matrix2).astype(np.uint8)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
images = [img, img_lower, img_higher1, img_higher2]
titles = [
    "Original",
    "Lower Contrast (0.8)",
    "Higher Contrast (1.1)",
    "Higher Contrast (1.2)"
]

plt.figure(figsize=(16, 5))

for i in range(4):
    plt.subplot(1, 4, i + 1)
    plt.imshow(cv2.cvtColor(images[i], cv2.COLOR_BGR2RGB))
    plt.title(titles[i])
    plt.axis("off")

plt.tight_layout()
plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
B, G, R = cv2.split(img)

plt.figure(figsize=(15, 5))

for i, (channel, title) in enumerate([
    (B, "Blue Channel"),
    (G, "Green Channel"),
    (R, "Red Channel")
]):
    plt.subplot(1, 3, i + 1)
    plt.imshow(channel, cmap="gray")
    plt.title(title)
    plt.axis("off")

plt.tight_layout()
plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_bgr = cv2.merge([B, G, R])
merged_rgb = cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(merged_rgb)
plt.title("Merged BGR Image")
plt.axis("off")

plt.tight_layout()
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
H, S, V = cv2.split(hsv)

plt.figure(figsize=(15, 5))

for i, (channel, title) in enumerate([
    (H, "Hue Channel"),
    (S, "Saturation Channel"),
    (V, "Value Channel")
]):
    plt.subplot(1, 3, i + 1)
    plt.imshow(channel, cmap="gray")
    plt.title(title)
    plt.axis("off")

plt.tight_layout()
plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge([H, S, V])
merged_bgr_hsv = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)
merged_hsv_rgb = cv2.cvtColor(merged_bgr_hsv, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(merged_hsv_rgb)
plt.title("Merged HSV Image")
plt.axis("off")

plt.tight_layout()
plt.show()
```

## Output:
<img width="843" height="583" alt="image" src="https://github.com/user-attachments/assets/046f51c6-bba5-4a37-b124-ac1ee576ccaf" />

<img width="1065" height="685" alt="image" src="https://github.com/user-attachments/assets/f26f2307-1a50-4a06-9750-366d952deeb8" />

<img width="656" height="520" alt="image" src="https://github.com/user-attachments/assets/501b2d7a-9f10-407f-b269-fe13e16bd19c" />

<img width="681" height="518" alt="image" src="https://github.com/user-attachments/assets/8a1a7c74-7f73-4344-b635-c244f89ebd2a" />

<img width="728" height="521" alt="image" src="https://github.com/user-attachments/assets/7ebf995e-b6c0-4088-91d2-00adae038815" />

<img width="940" height="666" alt="image" src="https://github.com/user-attachments/assets/d606f7e5-cf98-4b38-8300-47c06769315c" />

<img width="998" height="712" alt="image" src="https://github.com/user-attachments/assets/8201096f-d2aa-4207-bfa6-be644397bebd" />

<img width="392" height="520" alt="image" src="https://github.com/user-attachments/assets/90f8d419-d050-485b-98fe-f835bf4d4623" />

<img width="1362" height="522" alt="image" src="https://github.com/user-attachments/assets/283fa1cc-c3d0-4a1b-aacb-8d953dc0c18c" />

<img width="1365" height="443" alt="image" src="https://github.com/user-attachments/assets/23bfd469-d3e5-45b6-8fca-6bedc7515bf0" />

<img width="1355" height="517" alt="image" src="https://github.com/user-attachments/assets/51159695-dbc0-49aa-a38c-b304301dc5dd" />

<img width="1037" height="625" alt="image" src="https://github.com/user-attachments/assets/bbc4ac11-0c58-4835-b73b-403c0296e91f" />

<img width="1361" height="520" alt="image" src="https://github.com/user-attachments/assets/b578c953-02f5-4d0f-bde9-e128945e8220" />

<img width="1041" height="622" alt="image" src="https://github.com/user-attachments/assets/887bb950-438c-43ee-9cc1-14b7c47b1b68" />

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

