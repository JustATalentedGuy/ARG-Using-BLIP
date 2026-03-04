# 🩻 Automatic Radiology Report Generation using BLIP

## 📌 Overview

Radiology report generation is a crucial component of medical imaging workflows. However, interpreting medical images and drafting diagnostic reports is time-consuming and cognitively demanding for radiologists.

This project presents an **automatic radiology report generation system** built using the **BLIP (Bootstrapping Language–Image Pre-training)** developed by **Salesforce**.

The model is fine-tuned on paired chest X-ray images and their corresponding diagnostic reports to generate clinically meaningful descriptions.

The system achieves strong performance across multiple evaluation metrics, demonstrating the potential of vision–language models in assisting radiologists and improving clinical efficiency.

---

## 🧠 Model Architecture

* Base Model: `Salesforce/blip-image-captioning-base`
* Framework: PyTorch + HuggingFace Transformers
* Task: Image → Radiology Report Generation
* Max Report Length: 30 tokens
* Decoding: Beam Search (num_beams = 3)
* Fine-tuning: Teacher Forcing with Cross-Entropy Loss

BLIP is a transformer-based vision–language model designed for:

* Image Captioning
* Visual Question Answering
* Image–Text Retrieval

In this project, it is adapted for **medical image-to-report generation**.

---

## 📂 Dataset

The model is trained using:

* Chest X-ray images (.png)
* Corresponding diagnostic reports (.txt)

The dataset can be found [here](https://www.kaggle.com/datasets/raddar/tuberculosis-chest-xrays-shenzhen)

### Dataset Structure

```
ChinaSet_AllFiles/
│
├── diseased/
│   ├── image_1_1.png
│   ├── image_1_1.txt
│   └── ...
│
├── normal/
│   ├── image_2_0.png
│   ├── image_2_0.txt
│   └── ...
```

### Preprocessing

* Images resized to **224×224**
* Reports lowercased and cleaned
* Maximum token length: 30
* Train / Validation split: 80% / 20%

---

## ⚙️ Installation

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/JustATalentedGuy/ARG-Using-BLIP
cd ARG-Using-BLIP
```

### 2️⃣ Install Dependencies

```bash
pip install torch torchvision transformers
pip install nltk rouge-score scikit-learn
pip install pandas matplotlib seaborn tqdm
```

### 3️⃣ Download NLTK WordNet

```python
import nltk
nltk.download("wordnet")
```

---

## 🚀 Training Configuration

| Parameter     | Value               |
| ------------- | ------------------- |
| Optimizer     | Adam                |
| Learning Rate | 1e-5                |
| Batch Size    | 4                   |
| Epochs        | 10                  |
| Device        | CUDA (if available) |

Model checkpoint is saved as:

```
blip_captioner_finetuned.pth
```

---

## 📊 Evaluation Metrics

The generated reports are evaluated using standard NLG metrics:

| Metric      | Score      |
| ----------- | ---------- |
| BLEU        | **0.5859** |
| METEOR      | **0.4021** |
| ROUGE       | **0.6780** |
| RadGraph-F1 | **0.6424** |

### Metric Explanation

* **BLEU** – N-gram precision
* **METEOR** – Precision + recall with synonym matching
* **ROUGE-1 / ROUGE-2 / ROUGE-L** – Overlap with reference reports
* **RadGraph-F1** – Clinical entity & relation correctness

Evaluation outputs:

* CSV file with per-image metrics
* BLEU score distribution histogram

---

## 🏥 Clinical Significance

This system:

* Assists radiologists in drafting preliminary reports
* Reduces reporting time
* Improves workflow efficiency
* Produces consistent, structured descriptions

⚠️ **Disclaimer:**
This model is intended for research purposes only and should not be used for direct clinical decision-making without professional validation.

---

## 🔮 Future Improvements

* Increase report length capacity
* Use larger BLIP variants
* Integrate domain-specific medical tokenizers
* Incorporate RadGraph-based training objectives
* Extend to multi-view and multi-modal datasets
* Compare with models such as:

  * ViLT
  * GIT
  * BioGPT

---

## 📚 Citation

```
@INPROCEEDINGS{11407634,
  author={R, Ponsubash Raj and E, Thenmozhi and P, Mirunalini},
  booktitle={2026 9th International Conference on Computational Intelligence in Data Science (ICCIDS)}, 
  title={Automatic Generation of Medical Imaging Diagnostic Report using BLIP Model}, 
  year={2026},
  volume={},
  number={},
  pages={1-5},
  keywords={Radiology Report Generation;Chest X-ray Analysis;Vision-Language Models;BLIP;Medical Image Captioning;Healthcare AI},
  doi={10.1109/ICCIDS69108.2026.11407634}}
```
---
