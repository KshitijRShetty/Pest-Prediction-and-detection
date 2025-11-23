# Pest-Prediction-and-detection
# Pest Detection with YOLOv8

This project builds and trains a YOLOv8 object detection model to detect agricultural pests from images.  
The workflow is implemented in a single Jupyter notebook and includes:

- Inspecting the raw pest image dataset
- Sampling images per class for manual annotation
- Automatically generating bounding-box labels (pseudo-labels) using simple image processing
- Converting the data into YOLO format (train/val/test with `images/` and `labels/`)
- Training and evaluating a YOLOv8 model on 19 pest classes

## Dataset and Classes

The dataset consists of images of 19 pest classes. These are defined in `data/det_pseudo/data.yaml`:

- Adristyrannus  
- Aphids  
- Beetle  
- Bugs  
- Cabbage Looper  
- Cicadellidae  
- Cutworm  
- Earwig  
- FieldCricket  
- Grasshopper  
- Mediterranean fruit fly  
- Mites  
- RedSpider  
- Riptortus  
- Slug  
- Snail  
- Thrips  
- Weevil  
- Whitefly  

> Note: In your local environment, `data.yaml` may contain absolute Windows paths (e.g. `C:\Users\...`).  
> For portability, you should change these to relative or POSIX-style paths (e.g. `data/det_pseudo/train/images` etc.) after cloning.

## Project Structure

Key files and folders:

- `MAIN.ipynb`  
  Main notebook containing the full pipeline:
  - Dataset inspection
  - Sampling images for manual annotation (`data/annotation_sample`)
  - Automatic labeling with a contour-based algorithm (`data/auto_labels_simple`)
  - Building YOLO-format datasets (`data/det_auto`, `data/det_pseudo`)
  - Training and evaluating YOLOv8

- `data/`
  - `annotation_sample/`  
    Sampled images per class for manual annotation tools (e.g. LabelImg).
  - `auto_labels_simple/`  
    Automatically generated YOLO labels using simple thresholding + biggest contour.
  - `det_auto/`  
    YOLO-format dataset (train/val/test) built from the auto labels.
  - `det_pseudo/`  
    YOLO-format dataset with `images/`, `labels/`, and `data.yaml` used for training/inference.
  - `pseudo_labels/`  
    Additional intermediate pseudo-labels.

- (Optional, usually **not** committed)
  - `archive/` / `archive.zip` – original/raw dataset.
  - `runs/` – training logs and model checkpoints produced by YOLOv8.

## Requirements

You will need:

- Python 3.9+ (recommended)
- Jupyter Notebook or JupyterLab
- Common scientific + CV libraries

Minimal dependencies (adjust to your setup):

```bash path=null start=null
pip install ultralytics opencv-python tqdm matplotlib pyyaml jupyter
