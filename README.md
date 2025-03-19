# VR_Assignment1_AshashreeSarma_MS2024005

# Computer Vision Assignment: Coin Detection and Panorama Creation

This repository contains the implementation of two computer vision tasks:
1. Detection and segmentation of Indian coins
2. Creation of panoramic images from overlapping photos

## Project Structure

```
VR_Assignment1_AshashreeSarma_MS2024005/
├── src/
│   ├── coin_detection_and_segmentation.py
│   └── panorama.py
├── images/
│   ├── coins/
│   │   └── coinss.31.33 AM.png
│   └── panorama/
│       ├── a.jpeg
│       ├── b.jpeg
│       ├── c.jpeg
│       └── d.jpeg
├── results/
│   ├── coin_detection.png
│   ├── coin_segmentation.png
│   └── panorama_result.png
└── README.md
```

## Dependencies

The project requires the following Python packages:
```
opencv-python>=4.8.0
numpy>=1.24.0
matplotlib>=3.7.0
```

To install dependencies:
```bash
pip install -r requirements.txt
```

## Part 1: Coin Detection and Segmentation

### Implementation Details

The coin detection system follows a systematic approach to ensure accurate results:

1. **Grayscale Conversion**
   - Converts the image to grayscale to simplify processing and reduce computational load.
   - If omitted, color variations in coins and the background might interfere with edge detection, making the detection process unreliable.

2. **Gaussian Blur**
   - Applies a smoothing effect to remove noise, making coin boundaries clearer.
   - Without blurring, small textures and noise might create false detections, resulting in incorrect coin counting and segmentation.

3. **Edge Detection using Hough Circle Transform**
   - Detects circular objects (coins) by identifying contours and radius consistency.
   - If skipped, the system would struggle to differentiate between coins and non-circular objects, leading to false positives.

4. **Region-based Segmentation**
   - Isolates detected coins using binary masks to extract individual coins.
   - Without segmentation, overlapping coins or background noise may interfere with clear coin extraction.

### Features
1. **Coin Detection**
   - Uses edge detection with Hough Circle Transform to locate coins.
   - Green circles mark detected coins.
   - Adaptive parameter tuning for varying coin sizes.

2. **Segmentation**
   - Extracts individual coins using binary masks.
   - Background removal for clearer visualization.
   - Isolated coin images stored separately.

3. **Coin Counting**
   - Automatically counts detected coins.
   - Displays the total count in the console.
   - Segmented output verifies count accuracy.

#### Processing Flowchart:
```
[Input Image] → [Grayscale Conversion] → [Gaussian Blur] → [Edge Detection] → [Coin Detection] → [Segmentation] → [Coin Counting]
```

### How to Run

```bash
python src/coin_detection_and_segmentation.py
```

or run the script in Google Colab after uploading the images. Paths are predefined, requiring no additional configuration.

For VS Code execution, ensure images are placed in the correct directory structure as specified above.

### Results

The script produces three main outputs:
1. **Original image** with detected coins outlined in green.
2. **Segmented image** isolating the coins.
3. **Individual extracted coin images.**
4. **Total coin count displayed in the console.**

<p float="left">
  <img src="results/Coin Detection.png" width="500" />
  <img src="results/Coin Segmentation.png" width="500" />
</p>

Current detection accuracy: ~101 coins detected.

### Challenges Faced
- **Overlapping Coins**: Some coins are difficult to detect if they overlap significantly, leading to undercounting or incorrect segmentation. More sophisticated segmentation techniques, such as watershed or deep learning-based methods, could help address this issue.
- **Lighting Variations**: Uneven lighting affects segmentation and edge detection accuracy, causing missed detections or false positives. Adaptive thresholding or contrast enhancement techniques may improve performance.
- **Coin Reflection & Shadows**: Bright reflections can cause false detections, while shadows may obscure coin edges. Preprocessing techniques like histogram equalization could help balance illumination conditions.
- **Different Denominations**: Some coins may have low contrast, making detection harder, especially if they blend with the background. Feature-based classification methods might be required for better robustness.

### Further Improvements
- Implement **Deep Learning-based object detection** (e.g., YOLO, Faster R-CNN) for better accuracy.
- Improve segmentation using **watershed algorithms** or **active contours**.
- Enhance robustness under poor lighting conditions using adaptive preprocessing.

---

## Part 2: Panorama Creation

### Implementation Details

The panorama creation system utilizes:

1. **ORB (Oriented FAST and Rotated BRIEF)**
   - Detects keypoints and extracts feature descriptors.
   - If omitted, the system would lack critical features for alignment, making it impossible to match images effectively.

2. **BFMatcher (Brute Force Matcher)**
   - Matches feature descriptors between overlapping images.
   - Without it, images would not align properly due to a lack of correspondence, resulting in disjointed or misaligned panoramas.

3. **Homography Estimation (RANSAC)**
   - Computes transformations to align images, filtering out incorrect matches.
   - If skipped, image warping would be inaccurate, causing severe misalignment in the final panorama.

4. **Warping & Blending**
   - Warps images into a common perspective and blends overlapping regions.
   - Without proper blending, seams and artifacts would appear in the final panorama, making it visually unappealing.

### Features
1. **Keypoint Detection**
   - Uses ORB instead of SIFT (as SIFT is patented) for efficient feature detection.
   - Extracts keypoints and descriptors for image matching.

2. **Image Matching**
   - Matches keypoints using BFMatcher with Hamming distance.
   - Filters out bad matches to retain only strong correspondences.

3. **Image Stitching**
   - Computes a homography matrix for perspective transformation.
   - Warps images to align overlapping regions.
   - Blends images to create a seamless panorama.

#### Processing Flowchart:
```
[Input Images] → [Keypoint Detection] → [Feature Matching] → [Homography Computation] → [Warping] → [Blending] → [Final Panorama]
```

### Challenges Faced
- **Poor Feature Detection**: ORB does not always provide as strong matches as SIFT, leading to incorrect alignments. Using advanced feature extractors could improve matching.
- **Lighting Variations**: Differences in exposure can create visible seams in the panorama. Exposure correction techniques could mitigate this issue.
- **Insufficient Overlap**: If images have too little overlap, homography estimation fails, breaking the panorama. Capturing images with more overlap can help.
- **Perspective Distortion**: Wide-angle images can lead to unwanted distortions, making the stitched output unnatural. Applying cylindrical or spherical projections might improve results.
