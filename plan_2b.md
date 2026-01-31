# structure_2b.md
# 2b_[sign_attribute]_[student].ipynb
# Note: Each student completes ONE 2b notebook.
# In this project plan, 2b trains and evaluates ONLY ONE detector (chosen from that student's two 2a detectors).

##### PLS TRY DO ALL GRAPHS USING SEABORN (CLEANER THAN MATPLOTLIB)

## Section 0: Notebook Metadata and Configuration
- Course, task, student
- Selected attribute: [ATTRIBUTE_NAME]
  - viewing_angle OR mounting_type OR sign_condition OR sign_shape_type
- Selected detector for attribute training: [DETECTOR_FOR_ATTRIBUTE]
  - must be one of the student's 2a detectors
- Framework: PyTorch-based
- Dataset paths:
  - dataset/COCO-based_COCO_[ATTRIBUTE_NAME]/annotations/{train,val,test}.json
  - dataset/COCO-based_COCO_[ATTRIBUTE_NAME]/images/{train,val,test}/
- Output paths:
  - work_dirs/[detector_name]_[attribute_name]/
- Reproducibility:
  - fixed seed 
- Training budget:
  - epochs in range 10-25 (suggest 12 as a default starting point)
  - batch size chosen to fit GPU memory (document final value)

## Section 1: Environment Setup (PyTorch + Logging)
- Imports:
  - torch, torchvision (as needed)
  - numpy, pandas
  - matplotlib, seaborn
  - tensorboard utilities
  - detector framework imports (PyTorch-based)
- Print minimal environment info:
  - PyTorch version, CUDA availability, GPU name
  - framework version
- Set seeds for:
  - python random, numpy, torch (and torch cuda)

## Section 2: Dataset Validation 
- Validate annotation JSON and image directories exist for train/val/test
- Load COCO JSON and print counts only:
  - number of images, number of annotations, attribute class names
- Confirm NUM_CLASSES matches the attribute label set
- (optional) Show 1-2 images with GT boxes to confirm loading

## Section 3: Model Setup and Configuration (PyTorch)
- State the chosen detector architecture and why it is reused for attribute classification
- Load pretrained weights where applicable
- Configure:
  - num_classes = number of attribute classes
  - input size / resize policy
  - optimizer and learning rate
  - epochs (10-25) and batch size
- Document any default augmentations used

### TensorBoard Logging
- Ensure TensorBoard logging is enabled and point to log directory
- Print the exact command needed to view logs, for example:
  - tensorboard --logdir work_dirs/[detector_name]_[attribute_name]/

## Section 4: Training
- Train the model for the chosen number of epochs
- Track validation metrics during training (at least once per epoch)
- Save:
  - best checkpoint (by validation mAP or equivalent)
  - last checkpoint
- Record total training time

## Section 5: Test Set Evaluation (COCO Metrics)
- Load best checkpoint
- Evaluate on the TEST split
- Report overall metrics table:
  - mAP, AP50, AP75
- Report per-class AP table
- Plot per-class AP bar chart (for 3+ classes)

## Section 6: Training Curves and Monitoring
- Plot:
  - training loss curve(s)
  - validation mAP vs epoch
  - highlight best epoch
- If multiple losses exist, plot total loss if available; otherwise plot 2-3 main components with labels

## Section 7: Qualitative Results and Failure Analysis (Attribute)
- Run inference on selected TEST images
- Show a small grid of predictions including:
  - correct attribute predictions
  - challenging cases (distance, occlusion, glare, ambiguous angle/condition)
  - failure cases with short diagnosis
- (optional) Confidence score histogram using the same subset of images used for analytics/speed measurement
- (optional) Precision-recall curve if framework provides it with minimal extra work
- (optional) Confusion matrix only if framework outputs it automatically and you can interpret it correctly

## Section 8: Per-Image Analytics (Attribute-Oriented Output)
- Implement a function that, for each image:
  - counts detections above a fixed threshold (e.g., 0.5)
  - provides breakdown by the chosen attribute classes
  - computes mean confidence
- Run on a fixed set of 10 TEST images (fixed seed)
- Present as a table (pandas DataFrame)

## Section 9: Inference Speed Measurement
- Standard protocol:
  - device: GPU
  - batch size: 1
  - warmup iterations (e.g., 10)
  - timed iterations (e.g., 100 images)
- Report:
  - mean latency (ms), std latency (ms), FPS
- Note whether preprocessing is included in timing

## Section 10: Results Export for 2c Comparison
- Export results_export.json into:
  - work_dirs/[detector_name]_[attribute_name]/results_export.json
- Use the same standardized schema as 2a notebooks (consistent keys)
- Include model complexity (safe + comparable):
  - num_parameters
  - model_size_mb
  - flops (optional but I would try)
- Include speed protocol fields:
  - includes_preprocessing
  - num_warmup

## Section 11: Summary Discussion (Concise)
- Attribute-specific difficulty and what the results show
- Dominant failure modes and likely causes (link to dataset observations if relevant)
- Practical implications for monitoring (attribute analytics usefulness)
- Short limitations and practical improvements
