# structure_2c.md

##### PLS TRY DO ALL GRAPHS USING SEABORN (CLEANER THAN MATPLOTLIB)

## Section 0: Configuration
- Define team members
- Use glob to find all results_export.json files
- Group by task

## Section 1: Load and Validate Results
- Glob: work_dirs/**/results_export.json
- Load each JSON
- Validate schema (check required fields)
- Group by task: sign_type, viewing_angle, mounting_type, etc.
- Print:
  [INFO] Loading results...
  [INFO]   sign_type: Loaded N models
  [INFO]   viewing_angle: Loaded N models
  [INFO] All results validated

## Section 2: Sign Type Detection Comparison
- Build comparison dataframe
- Print table (use .to_string() for ASCII)
- Generate charts (matplotlib + seaborn):
  - overall mAP bar chart
  - speed vs accuracy scatter
  - grouped per-class AP comparison
- Save to: outputs/comparison/

## Section 3: Attribute Detection Comparisons
- Loop through each attribute
- Generate comparison table and charts per attribute
- Save to: outputs/comparison/

## Section 3.5: Same-Family Detector Comparison (If Applicable)
- Trigger: if multiple models belong to the same family (e.g., YOLOv8 vs YOLOv12)
- Produce a focused comparison:
  - delta mAP, delta FPS, delta params, delta model size
  - efficiency metrics (e.g., mAP per FPS, mAP per parameter)
- Charts (matplotlib + seaborn):
  - side-by-side per-class AP (where available)
  - speed vs accuracy scatter (highlight family)
- Short discussion:
  - what improved, what tradeoff occurred, best deployment choice

## Section 4: Architecture Analysis
- Markdown discussion (200-300 words):
  - two-stage vs single-stage tradeoffs observed
  - focal loss impact (if attribute had imbalance)
  - framework differences (PyTorch tooling differences across implementations)
  - small object detection insights (reference Notebook 1 bbox analysis)

## Section 5: Deployment Recommendations
- Best for high accuracy: [model] (mAP: X.XX, FPS: X.X)
- Best for real-time: [model] (FPS: XX.X, mAP: X.XX)
- Best balance: [model]
- Attribute-specific recommendations

## Section 6: Summary
- Save comparison_summary.json
- Print: [INFO] Comparison analysis complete
