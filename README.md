# TR Labs DS Challenge

This repository contains the code and artifacts for the Thomson Reuters Data Science Challenge: multi-label classification of judicial decisions into procedural postures.

## Project Structure
```
tr_labs_ds_challenge/
├── data/
│   ├── TRDataChallenge2023.txt      # Raw text dataset
│   ├── cleaned_filtered_data.json   # Filtered & preprocessed data
│   └── unlabeled_docs.jsonl         # Documents for inference
├── models/
│   ├── train_embeddings.pt          # Precomputed training embeddings
│   ├── val_embeddings.pt            # Precomputed validation embeddings
│   ├── classifier_head_precomputed.pth # Trained classifier weights
│   └── label_to_idx.pkl             # Mapping from posture labels to indices
├── notebooks/
│   ├── data_exploration_and_eda.ipynb    # EDA and preprocessing
│   ├── precompute_embeddings.ipynb       # Embedding computation
│   ├── train_classifier_from_embeddings.ipynb # Classifier training
│   └── inference.ipynb                   # Jupyter-based inference example
├── outputs/
│   ├── label_distribution.png            # Label frequency plot
│   ├── num_postures_distribution.png     # Number of labels per document
│   ├── posture_availability_pie.png      # Label availability pie chart
│   └── word_count_distribution.png       # Document length distribution
├── reports/
│   └── report.txt                        # Summary report of findings
├── utils/
│   ├── __init__.py                       # Python package marker
│   ├── data_utils.py                     # Data loading & preprocessing utilities
│   ├── embedding_utils.py                # Embedding helper functions
│   ├── label_utils.py                    # Label mapping & filtering
│   └── model_utils.py                    # Model definition & evaluation
├── inference.py                          # Command-line inference script
├── requirements.txt                      # Python dependencies
└── README.md                             # This file
```

## Prerequisites
- Python 3.8 or higher
- `pip` package manager
- (Optional) A virtual environment tool such as `venv` or `conda`

## Installation
1. Clone or extract the project ZIP:
   ```bash
   unzip tr_labs_ds_challenge.zip && cd tr_labs_ds_challenge
   ```
2. (Optional) Create and activate a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate      # macOS/Linux
   venv\Scripts\activate       # Windows
   ```
3. Install dependencies:
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

## Data
- **`data/TRDataChallenge2023.txt`**: Original raw dataset.
- **`data/cleaned_filtered_data.json`**: Filtered dataset with top labels and cleaned headtexts.
- **`data/unlabeled_docs.jsonl`**: JSONL file for running inference (each line: `{"document_id": ..., "text": ...}`).

## Usage

### 1. (Optional) Precompute Embeddings - if starting from raw data
```bash
python notebooks/precompute_embeddings.ipynb
```

### 2. (Optional) Train Classifier - if retraining
```bash
python notebooks/train_classifier_from_embeddings.ipynb
```

### 3. Run Inference
To generate predicted postures on new documents, use the command-line script:
```bash
python inference.py --input_json ./data/unlabeled_docs.jsonl
```
- **`--input_json`**: Path to the JSONL file containing documents to label.

### 4. View Results
- **Predictions**: See `predictions.jsonl` for each document's predicted postures.
- **Reports & Plots**: Check the `outputs/` directory for distribution plots and `reports/report.txt` for a summary.

## Notebooks
- **`data_exploration_and_eda.ipynb`**: Exploratory Data Analysis and preprocessing steps.
- **`inference.ipynb`**: Interactive example of running inference and visualizing results.

## Utilities
All reusable functions live in the `utils/` package:
- **`data_utils.py`**: Data loading, cleaning, and splitting.
- **`embedding_utils.py`**: Embedding model loading and vectorization.
- **`label_utils.py`**: Label indexing, filtering, and conversion.
- **`model_utils.py`**: Model architecture, loading, and evaluation metrics.
