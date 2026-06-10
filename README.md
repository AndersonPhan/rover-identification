# Rover Yolov5 Object Detection

## Introduction

This machine learning model was created and impemented on an autnomous navigating mapping rover that utilizes slam. One problem that the rover had was that it was 
unable to differentiate between obstacles using only its LiDAR. This limitation makes the difficult for the rover to decide whether to drive over an object or 
around it.

To address this problem, I developed a computer vision-based object detection model using YOLOv5. The model identifies two key object classes: Wooden Block and Ramp.

<p align = "center">
  <img width="300" height="91" alt="image" src="https://github.com/user-attachments/assets/daccb672-ea80-49d5-a4c4-1a6bc36c585c" />
</p>

## Dataset

The dataset was created by extracting frames from recorded videos of the rover environment. These images were manually annotated on a platform called Roboflow to 
identify ramps and wooden blocks. The annotated dataset can be seen in the Figure below with each object being highlighted in each input image:

<p align="center">
  <img width="465" height="314" alt="image" src="https://github.com/user-attachments/assets/bb8f0293-9823-4525-8150-96f25099eff8" />
</p>

### Object Classes

- Wooden Block
- Ramp

### Dataset Features:

Several factors were taken account into each image for a richer and more diverse dataset:

- Different camera angles of the objects
- Varying light levels
- Diverse object textures

## Model Training

The model was trained using **Google Colab**, which provided GPU acceleration for faster training.

### Training Config

| Parameter | Value |
|------------|--------|
| Epochs | 150 |
| Batch Size | 16 |
| Training Time | Approximately 30 minutes |

During training, the model learns to:

1. Identify objects within an image.
2. Classify each object as either a ramp or a wooden block.
3. Generate bounding boxes around detected objects.

## Testing and Results

The trained YOLOv5 model processes incoming camera images and outputs:

- Object class labels
- Bounding box locations
- Detection confidence scores

The model can be seen being executed in the Figure below:

<p align="center">
  <img width="466" height="305" alt="image" src="https://github.com/user-attachments/assets/ba3e83d7-8b63-473d-8493-2551a11cf372" />
</p>

### Model Performance

Model performance was evaluated using standard object detection metrics, including:

- Mean Average Precision (mAP)
- Precision
- Recall

These metrics were graphed and visualized using Weights and Biases and can be found in the Figure below:

<p align="center">
  <img width="469" height="228" alt="image" src="https://github.com/user-attachments/assets/3639c3e6-a985-4514-9c04-e2751a611dc7" />
</p>

### Model Implementation

After the YOLOv5 model was trained in Google Colab, the resulting best.pt file containing the trained weights was exported and transferred to the rover's 
Raspberry Pi. The Raspberry Pi executes the object detection model in real time using a connected camera as the primary input source.

The implementation consists of three main components:

- A camera for capturing live video of the rover's surroundings.
- The YOLOv5 object detection script running on the Raspberry Pi.
- The ROS visualization tool rqt, which displays the camera feeds and detection results.

As shown in the figure below, the left side displays the live camera feed captured by the rover. The right side displays the processed video stream at a 
reduced frame rate, allowing sufficient computational resources for the YOLOv5 model to perform object detection accurately. The model successfully 
identifies wooden blocks within the environment and places green bounding boxes around the detected objects.

<p align="center">
  <img width="537" height="300" alt="image" src="https://github.com/user-attachments/assets/109c116a-4cfe-4535-9dc3-985f93dac252" />
</p>
