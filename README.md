# Moving Object Detection

A real-time motion detection application built with OpenCV that captures video from your webcam and identifies moving objects in the frame.

## Overview

This project implements a motion detection system using background subtraction techniques. It captures video frames, processes them to detect changes between consecutive frames, and highlights moving objects with bounding boxes.

## Features

- **Real-time motion detection** - Detects movement from webcam feed
- **Visual feedback** - Draws green bounding boxes around moving objects
- **Status indicator** - Displays "Moving object Detected" or "Normal" on screen
- **Adjustable sensitivity** - Configurable area threshold to filter out small movements
- **Gaussian blur** - Reduces noise for more accurate detection
- **Frame differencing** - Compares current frame with the first captured frame

## Technical Implementation

### Key Components

- **Frame Capture**: Uses OpenCV's `VideoCapture` to access webcam (device 0)
- **Preprocessing**: Converts to grayscale and applies Gaussian blur (21x21 kernel)
- **Background Model**: Stores the first frame as the reference background
- **Difference Calculation**: Computes absolute difference between current and background frames
- **Thresholding**: Binary threshold (25-225) to identify motion regions
- **Dilation**: Expands detected regions to create more cohesive contours
- **Contour Detection**: Finds and filters contours based on minimum area (500 pixels)
- **Bounding Boxes**: Draws rectangles around detected moving objects

### Dependencies

- OpenCV (`cv2`)
- imutils


## Configuration Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `area` | 500 | Minimum contour area to detect (adjust for sensitivity) |
| `width` | 500 | Resized frame width (maintains aspect ratio) |
| `Gaussian kernel` | (21,21) | Blur kernel size for noise reduction |
| `Threshold` | 25-225 | Binary threshold range for motion detection |
| `Dilation iterations` | 2 | Number of dilation passes |

## How It Works

1. **Initialization**: Captures the first frame as the background reference
2. **Processing**: Each new frame is:
   - Resized and converted to grayscale
   - Blurred to reduce noise
   - Compared with the background frame
3. **Detection**: 
   - Pixels with significant differences are thresholded
   - Contours are extracted from the thresholded image
   - Contours larger than `area` trigger detection
4. **Output**: 
   - Green rectangles highlight detected objects
   - Text status updates on the video feed

## Potential Improvements

- Implement adaptive background modeling (MOG2 or KNN)
- Add object tracking (CentroidTracker)
- Implement motion history for better stability
- Add video recording capabilities
- Include distance estimation

