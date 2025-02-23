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
│   ├── Scattered_indian_coins_input_images/
│   │   └── coinss.31.33 AM.png
│   └── Panorama_captured_Images/
│       ├── a.jpeg
│       ├── b.jpeg
│       ├── c.jpeg
│       └── d.jpeg
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

The coin detection system uses the following techniques:
- Grayscale conversion for initial processing
- Gaussian blur for noise reduction
- Hough Circle Transform for coin detection
- Region-based segmentation for coin isolation

### Features
1. **Coin Detection**
   - Edge detection using Hough Circle Transform
   - Visual output with green circles marking detected coins
   - Handles varying coin sizes with adaptive parameters

2. **Segmentation**
   - Individual coin isolation using mask-based approach
   - Black background separation for clear visualization
   - Extraction of individual coin images

3. **Coin Counting**
   - Automatic counting of detected coins
   - Visual display of total count
   - Verification through segmented output

### How to Run

```bash
python src/coin_detection_and_segmentation.py

or sun the followimg file in collab
```

### Results

The script produces three main outputs:
1. Original image with detected coins outlined in green
2. Segmented image showing isolated coins
3. Individual extracted coins
4. Total coin count displayed in the console

<p float="left">
  <img src="path/to/image1.png" width="200" />
  <img src="path/to/image2.png" width="200" />
</p>


Current detection accuracy: ~95 coins detected

### Observations

- The system effectively detects most coins in clear view
- Current limitations with overlapping coins
- Performance affected by lighting conditions and coin orientation
- Consistent detection for coins of different denominations

## Part 2: Panorama Creation

### Implementation Details

The panorama creation system utilizes:
- SIFT (Scale-Invariant Feature Transform) for keypoint detection
- OpenCV's Stitcher class for image alignment and blending
- RGB/BGR color space conversion for proper visualization

### Features
1. **Keypoint Detection**
   - SIFT feature detection
   - Visual representation of keypoints
   - Rich keypoint visualization with size and orientation

2. **Image Stitching**
   - Automatic alignment of overlapping images
   - Seamless blending of multiple images
   - Error handling for failed stitching attempts

### How to Run

```bash
python src/panorama.py
```

### Results

The script produces:
1. Visualization of original input images
2. Images with detected keypoints
3. Final stitched panorama

### Observations

- Successful stitching requires sufficient overlap between images
- Best results achieved with consistent lighting and minimal movement
- SIFT provides robust feature detection across different scenes

## Known Issues and Future Improvements

1. Coin Detection:
   - Improve detection of overlapping coins
   - Add denomination classification
   - Enhance performance in varying lighting conditions

2. Panorama Creation:
   - Optimize memory usage for large images
   - Add support for vertical panoramas
   - Implement exposure compensation

## Author

[Your Name]
Roll No: [Your Roll No]

## License

This project is licensed under the MIT License - see the LICENSE file for details.
