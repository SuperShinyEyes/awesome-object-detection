# Awesome Object Detection

## YOLO (2016)

- Other than the size of the network, all training and testing parameters are the same between YOLO and Fast YOLO.
- Detection often requires fine-grained visual information so we increase the input resolution of the network from 224 × 224 to 448 × 448.
    - Train the classifier network with 224 × 224, and increase the resolution to 448 for detection
- Main source of error is incorrect localizations
- YOLO shares some similarities with R-CNN. 
    > Each grid cell proposes potential bounding boxes and scores those boxes using convolutional features
### Pros
- One-pass
- Look at whole image; reasons globally about the image when making predictions.
- Compared to SOTA, YOLO makes more localization errors but is less likely to predict false positives on background
    - YOLO makes less than half the number of background errors compared to Fast R-CNN.
- Speed: 45 fps, 150 fps on a Titan X
- YOLO makes far fewer background mistakes than Fast R-CNN.
    - You can get better detection by combining R-CNN and YOLO.

### Cons
- While it can quickly identify objects in im- ages it struggles to precisely localize some objects, espe- cially small ones
- Struggles with small objects. 
    > YOLO imposes strong spatial constraints on bounding box predictions since each grid cell only predicts two boxes and can only have one class. This spatial constraint limits the number of nearby objects that our model can predict. 
- Uses relatively coarse features for predicting bounding boxes since our architecture has multiple downsampling layers
- loss function treats errors the same in small bounding boxes versus large bounding boxes

### Question 🤔

- How does YOLO recognizes a center of an object?
    > Our system divides the input image into an S × S grid. If the center of an object falls into a grid cell, that grid cell is responsible for detecting that object.


--------
## YOLOv2 & YOLO 9000 (2017)

### Pros

### Cons


--------
## YOLOv3 (2018)
- Train on full images 
- Use multi-scale training, lots of data augmentation, batch normalization

### Pros
- More accurate
- When using old metric (mAP IOU = 0.5), it outperforms ResNet-101 and -152 in both accuracy and speed.

### Cons
- Larger: YOLOv2 had 19 conv layers. v3 has 53.
- With the new multi-scale predictions we see worse performance on medium and larger size objects. 


### About the new COCO metric and IOU threshold
- PASCAL VOC, the IOU threshold was ”set deliberately low to account for inaccuracies in bounding boxes in the ground truth data“. 
- Does COCO have better labelling than VOC? Possible since COCO has segmentation masks.
- COCO metric emphasizes better bounding boxes but that emphasis must mean it de-emphasizes something else, in this case classification accuracy.
    - I believe we often want more accurate classification than very accurate bbox predictions
- Performs very well on old metric (mAP IOU = 0.5). Performance drops significantly as the IOU threshold increases; struggles to get the boxes perfectly aligned with the object.


--------
## YOLOv4 (2020)
- Use new features:
    - Weighted-Residual-Connections (WRC), 
    - Cross-Stage-Partial-connections (CSP), 
    - Cross mini-Batch Normalization (CmBN), 
    - Self-adversarial-training (SAT) 
    - Mish-activation. 
    - Mosaic data augmentation, 
    - DropBlock regularization, 
    - CIoU loss

- Architecture:
    - backbone: CSPDarknet53
    - Neck: Spatial Pyramid Pooling (SPP), Path Aggregation Network (PAN)
    - HEAD: YOLOv3
### Pros

### Cons

