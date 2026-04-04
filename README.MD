# DL Midterm 2026: Text-to-SVG Generation

NYU Deep Learning Spring 2026 — ECE-GY 7123 / CS-GY 9223  
Kaggle competition: Text-to-SVG generation from natural language prompts.

**Team:** Ethan Bell (ecb10001@nyu.edu), Hivansh Dhakne (hd2296@nyu.edu)  
**Public leaderboard score:** 13.26  
**Model weights:** https://drive.google.com/drive/folders/1Ph7xE23PBqxwO55H2WoSzXfAR4tNjFvu  
**Competition:** https://www.kaggle.com/t/5c1b9c14c05c4bee82a0425c812e5ca4

---

## Start Here (For Grading)

To reproduce our final results:

- Final training notebook: `training/last-fintetune-run-V4.ipynb`
- Final inference notebook: `inference/kaggle-submission-v2.ipynb`

**Only the inference notebook is required to reproduce the final submission.**

---

## Expected Output

Running `inference/kaggle-submission-v2.ipynb` produces:

```
/kaggle/working/submission.csv
```

This is the file submitted to Kaggle for scoring.

---

## Reproducing the Final Submission (Kaggle)

The inference notebook is designed to run end-to-end on Kaggle. The competition data (`train.csv` and `test.csv`) is accessed directly through the Kaggle competition dataset.

### Steps

1. Join the competition using your NYU Kaggle account
2. Download the model weights folder from the Drive link above  
   - Rename the folder to: `final-model/`
3. Upload this folder as a Kaggle dataset  
   - Example name: `midterm-finetuned-model`
4. Open `inference/kaggle-submission-v2.ipynb` as a new Kaggle notebook
5. Under **Data**, attach:
   - The competition dataset  
   - Your uploaded model weights dataset
6. Set accelerator to **GPU (T4 x2)**
7. Run all cells

Inference completes in ~1 hour at batch size 50.

---

### Important Notes

- If your Kaggle dataset path differs, update the `adapter_path` variable in the first config cell of the notebook.
- No internet access is required after datasets are attached.
- Retraining is **NOT required** to reproduce results — use provided weights.

---

## Reproducing Locally or on Colab

### Install Dependencies

```bash
pip install -r requirements.txt
```

Tested on:
- Python 3.10+
- CUDA 12.x
- Google Colab (L4 GPU)
- Kaggle (T4 GPU)

---

### Data

Download `train.csv` and `test.csv` from Kaggle and place in your working directory.

---

### Training (Optional)

To retrain from scratch:

1. Place `train.csv` in:
   ```
   MyDrive/DL-midterm-2026/
   ```
2. Run:
   ```
   training/last-fintetune-run-V4.ipynb
   ```
3. Training takes ~3 hours on L4 GPU
4. Output saves to:
   ```
   final-model/
   ```

---

## Final Configuration

- Base model: Qwen2.5-Coder-3B-Instruct (4-bit)
- LoRA rank: 64
- LoRA alpha: 128
- Learning rate: 2e-4
- Epochs: 3
- Effective batch size: 64
- Max sequence length: 4096
- Seed: 42

---

## Repository Structure

```
dl-midterm/
├── README.md
├── requirements.txt
├── eda/
│   ├── eda-general-experiment-1.ipynb
│   └── eda_analysis.ipynb
├── training/
│   └── last-fintetune-run-V4.ipynb     # FINAL training run
└── inference/
    └── kaggle-submission-v2.ipynb      # FINAL submission notebook
```

### Notes on Removed Files

Only final notebooks are included for clarity and reproducibility.  
Earlier experimental runs and bugged checkpoints were removed to avoid confusion.

---

## Requirements

The `requirements.txt` file includes all necessary dependencies.

Make sure it contains (at minimum):

- transformers  
- peft  
- trl  
- bitsandbytes  
- unsloth (if used)  
- accelerate  
- datasets  
- pandas  
- numpy  

If running on Kaggle or Colab, GPU-compatible versions will install automatically.

---

## Additional Notes

- All experiments use seed = 42
- Model is trained using QLoRA (4-bit + LoRA adapters)
- Inference includes validation and constraint enforcement to avoid invalid SVG outputs

---

## AI Tooling Disclosure

Claude (Anthropic), ChatGPT (OpenAI), and Gemini (Google) were used for coding assistance and debugging.
