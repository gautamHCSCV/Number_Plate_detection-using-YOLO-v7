# Number_Plate_detection-using-YOLO-v7
YOLO is an algorithm that uses neural networks to provide real-time object detection. This algorithm is popular because of its speed and accuracy. It has been used in various applications to detect traffic signals, people, parking meters, and animals. YOLOv7 is the new state-of-the-art object detector in the YOLO family. According to the paper, it is the fastest and most accurate real-time object detector to date. According to the YOLOv7 paper, the best model scored 56.8% Average Precision (AP), which is the highest among all known object detectors.

## Sample Predictions
![test_batch0_pred](https://user-images.githubusercontent.com/65457437/191415063-e4eb5166-fa96-466f-a4d3-f18861176554.jpg)

![test_batch1_pred](https://user-images.githubusercontent.com/65457437/191415075-4f7ae712-0d4e-41c6-ac21-9c3cfdcc0716.jpg)

![inference video](https://github.com/gautamHCSCV/Number_Plate_detection-using-YOLO-v7/blob/main/Sample%20outputs/output_B.mp4)

Inference: !python detect.py --weights weights/yolov7.pt --conf 0.3 --save-txt --source inference/images
