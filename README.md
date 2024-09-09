# Therapist-and-Child-Detection-and-Tracking

This project involves detecting and tracking children and therapists in video footage using a combination of Grounding DINO for zero-shot object detection, FaceNet's Inception Resnet V1 for re-identification (ReID), and DeepSORT for multi-object tracking.

## Table of Contents

## Installation

To run this project, you need to have Python installed along with the required libraries. Follow the steps below to set up the environment.

pip install opencv-python-headless torch numpy facenet-pytorch deep_sort_realtime autodistill autodistill-grounding-dino

## Parameters
video_path: The path to the input video file.
output_path: The path where the output video with detections and tracking will be saved.
resize_factor: Factor by which to resize the video frames for faster processing (default is 0.5).
frame_skip: Number of frames to skip for faster processing (default is 5).

## How It Works

Zero-Shot Detection: The project uses Grounding DINO to detect children and therapists in video frames. This model is capable of zero-shot object detection based on predefined ontologies.

ReID (Re-Identification): After detecting the objects, the Inception Resnet V1 model from FaceNet is used to extract ReID features. These features help in consistently identifying the same person across different frames.

Tracking: The DeepSORT tracker uses the detections and ReID features to track the objects (children and therapists) across frames, assigning consistent IDs to each individual.

Results: The output video shows bounding boxes around detected individuals along with their assigned IDs, making it easier to track their movements throughout the video.

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
Execute the provided script in a Google Colab environment.
The processed video will be saved as output_video.mp4 with unique and consistent IDs assigned to each detected object.



