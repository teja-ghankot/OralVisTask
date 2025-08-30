# OralVis – Tooth Quadrant Detection using YOLOv8

This project trains a **YOLOv8** model to detect teeth quadrants in panoramic dental X-rays.  
Training and experiments were carried out in **Google Colab**.

---

## 📂 Project Structure
```
.
├── runs/                 # Training outputs (weights, logs, metrics)
├── OralVis.ipynb         # Colab notebook
├── data.yaml             # Dataset configuration file
└── README.md             # Documentation
```

---

## ⚙️ Environment Setup

Run the following inside Colab to install dependencies:
```bash
!pip install ultralytics
```

---

## 🚀 Training Command

Training was performed with:

```bash
!yolo detect train data=/content/drive/MyDrive/OralVis/dataset_split/data.yaml     model=yolov8s.pt epochs=100 imgsz=640 batch=16
```

- **data** → Dataset configuration file  
- **model=yolov8s.pt** → Pretrained YOLOv8 small model  
- **epochs=100** → Number of training epochs  
- **imgsz=640** → Input image size  
- **batch=16** → Batch size  

---

## 📊 Evaluation

Validation & testing were performed using:

```python
from ultralytics import YOLO

# Load best trained model
model = YOLO("runs/detect/train/weights/best.pt")

# Evaluate on test split
results = model.val(data="/content/drive/MyDrive/OralVis/dataset_split/data.yaml", split="test")
print(results)
```

---

## 📌 Post-Processing

- Split panoramic X-rays into **4 quadrants**.  
- Skipped gap regions to avoid false positives.  
- Applied **IDF values** to refine final predictions.  
- Visualized results with FDI tooth numbering.

---

## 🔗 References
- [Ultralytics YOLOv8 Docs](https://docs.ultralytics.com/)
- [YOLOv8 GitHub](https://github.com/ultralytics/ultralytics)
