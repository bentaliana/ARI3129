# ARI3129 - Advanced Computer Vision for Artificial Intelligence (Group Assignment)

<span style="font-size:1.5em;">
By Alison Attard, Ben Taliana, Melat Assefa & Michael Farrugia
</span>

Group 7  
University of Malta

This repository contains the code for the ARI3129 Group Assignment, where a dataset regarding Maltese traffic signs is compiled and used to train eight distinct object detection models to identify, locate and classify these signs (Notebooks 2a). These models include:
- CenterNet
- EfficientDet
- Faster R-CNN
- Mask R-CNN
- RetinaNet
- RF-DETR
- YOLOv8
- YOLOv12

Furthermore, four of these models are then used to perform localisation and classification of different attributes of the traffic signs, including mounting type, viewing angle, sign type, and sign conclusion (Notebooks 2b). These results are all compiled neatly into Notebook 2c for easy comparison.

To view the visualisation of the dataset, kindly refer to Notebook 1.

## Usage

To install the reqiured dependencies, run:

```bash
pip install -r requirements.txt
```

## File Structure

- `AlisonAttard/`: contains all files related to Alison Attard's implementation, including images and exports
- `BenTaliana/`: contains all files related to Ben Taliana's implementation, including images and exports
- `MelatAssefa/`: contains all files related to Melat Assefa's implementation, including images and exports
- `MichaelFarrugia/`: contains all files related to Michael Farrugia's implementation, including images and exports
- `dataset/`:
    - `COCO-based_COCO/`: contains the COCO-formatted dataset used for training and testing the models, including train-val-test splits
    - `COCO-based_COCO_condition/`: contains the COCO-formatted dataset for the condition attribute, including train-val-test splits
    - `COCO-based_COCO_mounting/`: contains the COCO-formatted dataset for the mounting type attribute, including train-val-test splits
    - `COCO-based_COCO_sign_shape/`: contains the COCO-formatted dataset for the sign shape attribute, including train-val-test splits
    - `COCO-based_COCO_view_angle/`: contains the COCO-formatted dataset for the viewing angle attribute, including train-val-test splits
    - `YOLO_COCO/`: contains the YOLO-formatted dataset used for training and testing the YOLO models, including train-val-test splits
    - `YOLO_COCO_condition/`: contains the YOLO-formatted dataset for the condition attribute, including train-val-test splits
    - `YOLO_COCO_mounting/`: contains the YOLO-formatted dataset for the mounting type attribute, including train-val-test splits
    - `YOLO_COCO_sign_shape/`: contains the YOLO-formatted dataset for the sign shape attribute, including train-val-test splits
    - `YOLO_COCO_view_angle/`: contains the YOLO-formatted dataset for the viewing angle attribute, including train-val-test splits
- `work_dirs/`: contains the saved model weights and logs for each model and attribute, including TensorBoard logs