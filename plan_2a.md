# structure_2a.md
# 2a_[object_detector_architecture_name]_[student].ipynb
# Note: Each student completes TWO separate 2a notebooks,
# one per chosen detector architecture, trained on the sign type dataset.

##### PLS TRY DO ALL GRAPHS USING SEABORN (CLEANER THAN MATPLOTLIB)

## Section 0: Notebook Metadata and Configuration
- Course, task, student, detector name
- Framework: PyTorch-based (e.g., Ultralytics YOLO in PyTorch, or MMDetection in PyTorch)
- Dataset paths:
  - dataset/COCO-based_COCO/annotations/{train,val,test}.json
  - dataset/COCO-based_COCO/images/{train,val,test}/
- Output paths:
  - work_dirs/[detector_name]_sign_type/
- Reproducibility:
  - fixed seed (I like to use the course code: 3129 ) 
  - deterministic flags where applicable
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
  - framework version (Ultralytics/MMDetection/etc.)
- Set seeds for:
  - python random, numpy, torch (and torch cuda)
- Create output directories

## Section 2: Dataset Validation 
- Validate that annotation JSON files exist for train/val/test
- Validate that image directories exist
- Load COCO JSON and print counts only:
  - number of images, number of annotations, class names
- (optional) Show 1-2 images with GT boxes purely to confirm correct loading

## Section 3: Model Setup and Configuration (PyTorch)
- State detector architecture and why chosen (short rationale)
- Load pretrained weights (COCO pretrained where applicable)
- Configure:
  - num_classes
  - input size / resize policy (document)
  - optimizer and learning rate (document)
  - epochs (10-25) and batch size (document)
- Data augmentation:
  - document what is enabled (default pipeline or explicit transforms)

### TensorBoard Logging
- Ensure TensorBoard logging is enabled and point to log directory
- Print the exact command needed to view logs, for example:
  - tensorboard --logdir work_dirs/[detector_name]_sign_type/

## Section 4: Training
- Train the model for the chosen number of epochs
- Track validation metrics during training (at least once per epoch)
- Save:
  - best checkpoint (by validation mAP or equivalent)
  - last checkpoint
- Record total training time (for later reporting)

## Section 5: Test Set Evaluation (COCO Metrics)
- Load best checkpoint
- Evaluate on the TEST split (not validation)
- Report overall metrics in a small table:
  - mAP, AP50, AP75
- Report per-class AP in a table
- Plot per-class AP bar chart (for 3+ classes)

## Section 6: Training Curves and Monitoring
- Use TensorBoard logs and/or exported scalars to plot:
  - training loss curve(s)
  - validation mAP vs epoch
  - highlight best epoch
- If multiple losses exist, plot total loss if available; otherwise plot 2-3 main components with labels

## Section 7: Qualitative Results and Failure Analysis
- Run inference on selected TEST images
- Show a small grid of predictions including:
  - clear successes
  - challenging cases (small signs, occlusion, glare, distance)
  - failure cases with short diagnosis
- Confidence score histogram using the same subset of images used for analytics/speed measurement
-  Precision-recall curve if the framework provides it with minimal extra work
- Confusion matrix only if the framework outputs it automatically and you can interpret it correctly

## Section 8: Per-Image Analytics 
- Implement a function that, for each image:
  - counts detections above a fixed threshold (e.g., 0.5)
  - provides breakdown by sign type
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
  - work_dirs/[detector_name]_sign_type/results_export.json
- Use a standardized schema across all notebooks (consistent keys)
- Include model complexity (safe + comparable):
  - num_parameters
  - model_size_mb
  - flops (optional, only if available easily)
- Include speed protocol fields:
  - includes_preprocessing
  - num_warmup

## Section 11: Summary Discussion (Concise)
- Convergence behavior (what epoch plateau occurred)
- Overall performance and per-class patterns
- Key failure modes and likely causes
- Practical implications (speed vs accuracy for monitoring use case)
- Short limitations and improvements (brief, practical)
