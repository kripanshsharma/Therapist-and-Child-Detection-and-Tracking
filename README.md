# Therapist-and-Child-Detection-and-Tracking

## Project Overview
This project aims to detect and track children and therapists in a video using a custom-trained YOLO model. The goal is to assign unique and consistent IDs to each detected person (either a child or a therapist) and maintain those IDs throughout the video. The solution involves processing each frame of the video, detecting objects, and ensuring that once an ID is assigned, it remains the same across all frames.

## Requirements
Python 3.x
Google Colab (or a similar environment)
Libraries:
OpenCV
Pandas
Ultralyitcs YOLOv8
Math
You can install the necessary Python packages using the following command:
  pip install ultralytics opencv-python-headless pandas
  
## Data Preparation
Custom YOLO Model: The model is trained to detect two specific classes: child and therapist. The trained model (your_custom_model.pt) must be placed in the same directory as the script.

Video File: The input video (your_video.mp4) should be placed in the same directory as the script. This video will be processed to detect and track the objects.

# Logic Behind the Analysis
## 1. Initialization
Tracker Class: The Tracker class is designed to handle the tracking and assignment of unique IDs. It maintains the center positions of detected objects and keeps track of assigned IDs across frames.

Attributes:
center_points: Stores the center points of detected objects.
id_count: A counter to assign unique IDs.
id_to_class: Maps the assigned ID to the detected object's class (either child or therapist).
tracked_objects: Keeps track of all detected objects and their assigned IDs across frames.

## 2. Model Prediction
Detection: For each frame in the video, the YOLO model is used to detect objects. The model outputs bounding boxes, confidence scores, and class IDs.

Class Filtering: Only objects classified as child or therapist are considered for further processing. The class_id is used to filter detections according to the trained classes.

## 3. Consistent ID Assignment
Tracking Logic: The center points of detected objects are compared with those from previous frames to determine if an object has been seen before. If the object is recognized (i.e., the center point is within a certain distance threshold), it retains its previously assigned ID.

New Object Detection: If an object is detected that does not match any existing objects (based on the center point comparison), a new unique ID is assigned.

Data Structure Updates: The center_points dictionary is updated with the current positions of objects, and the tracked_objects dictionary is updated to maintain consistent IDs across all frames.

## 4. Output Generation
Labeling: Each detected object is labeled with its assigned ID and class. For example, a child might be labeled as "ID 1 Child", and a therapist as "ID 2 Therapist".

Video Output: The processed video, with bounding boxes and labels drawn on each frame, is saved as output_video.mp4.

## 5. Error Handling
Index Validation: To prevent errors such as IndexError: list index out of range, the script includes a validation step to ensure that the class_id returned by the model is within the bounds of the class_list.

## 6. Reproducibility
Environment: The script is designed to run in a Google Colab environment, ensuring that all necessary dependencies are installed.

Debugging: The script includes optional print statements to assist in debugging and understanding the flow of data.

## 7. Expected Results
Consistent Tracking: The final output video should display consistent IDs for each person (child or therapist) throughout the video. This ensures that each individual is uniquely and accurately tracked, even as they move or re-enter the frame.
Running the Script

To reproduce the results:
Upload your your_custom_model.pt and your_video.mp4 to the working directory.
Execute the provided script in a Google Colab environment.
The processed video will be saved as output_video.mp4 with unique and consistent IDs assigned to each detected object.

## Conclusion
This project demonstrates a robust method for detecting and tracking objects in a video using a custom-trained YOLO model. By ensuring consistent ID assignment, the solution can effectively track individuals across video frames, making it suitable for applications like surveillance, behavioral studies, and more.

