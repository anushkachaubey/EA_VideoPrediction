
# Video Frame Prediction using Deep Learning on Moving MNIST

This project tackles video frame prediction on the Moving MNIST dataset using convolutional models — a Vanilla CNN and a deeper ResNet. The main evaluation metric is Structural Similarity Index (SSIM), which better captures perceptual quality than pixel-wise errors.

We compare several loss functions (MSE, BCE, Dice, Focal, and combined BCE + Dice) and find BCE + Dice loss (BCEDice) outperforms others by effectively handling the imbalanced background and digit pixels.

Different prediction settings are tested, including single-frame, multi-frame, and recursive prediction with scheduled sampling — a training strategy that gradually replaces ground truth frames with predicted ones to reduce exposure bias. Results show ResNet with BCEDice loss and scheduled sampling achieves the best SSIM and produces sharper, more stable frame predictions.

---

## 📁 Project Structure

```
EA_VideoPrediction_MNIST/
│
├── EA_VideoPrediction_MNIST.ipynb   # Main notebook with model training and evaluation
├── README.md                        # Project overview and usage guide
└── requirements.txt                 # Python dependencies
```

---

## 🧠 Methodology
**Dataset:** Moving MNIST — a synthetic dataset of MNIST digits moving inside a frame.

**Tasks**: The frame prediction pipeline was developed progressively to capture complex temporal patterns:

1. **Single-Frame Prediction:** Predict the next frame from one input frame to establish baseline performance.  
2. **Multi-Frame to Single Prediction:** Use 10 past frames to predict the next single frame, capturing richer motion context.  
3. **Multi-Frame to Multi-Frame Prediction:** Predict 5 future frames from 10 input frames, testing longer-term dynamics.  
4. **Recursive Prediction:** Feed predicted frames back as inputs to generate extended sequences, evaluating model robustness.  
5. **Scheduled Sampling:** Gradually replace ground truth inputs with predicted frames during training to reduce exposure bias and improve long-term predictions.

**Model Architecture:**
  - Encoder-Decoder style convolutional model with ConvLSTM layers.
  - Trained using BCE+Dice loss.
  - Evaluated using Structural Similarity Index (SSIM) for perceptual similarity.

**Evaluation:**
  - Average SSIM computed across predicted frames.
  - Frame-wise prediction accuracy assessed against ground-truth frames.

---

## 🔍 Key Findings

- Predicting multiple future frames improves once the model learns temporal progression and structural patterns.  
- Feeding the model’s own predicted frames back as inputs without training on this leads to significant performance drops due to error accumulation (e.g., ResNet SSIM dropped from 0.71 to 0.64).  
- Introducing **scheduled sampling**—gradually replacing ground truth frames with predicted frames during training—helps the model adapt to recursive prediction.  
- With scheduled sampling, the model recovers and surpasses original performance, reaching an SSIM of 0.78.  
- Scheduled sampling effectively bridges the gap between training and inference, improving long-term prediction stability and accuracy.

---

## ⚙️ How to Run

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/EA_VideoPrediction_MNIST.git
   cd EA_VideoPrediction_MNIST
   ```

2. **Create Environment and Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```
3. **Add Moving MNIST dataset**: https://www.kaggle.com/datasets/glandox/moving-mnist
4. **Run the Notebook**
   Open and run `EA_VideoPrediction_MNIST.ipynb` using Jupyter Notebook or VS Code. The notebook is fully self-contained.

---

## 📊 Metrics

- **SSIM (Structural Similarity Index):**
  - Computed per predicted frame.
  - Averaged over the 5-frame prediction horizon.
  - Measures perceptual similarity between predicted and ground-truth frames.

---

## 📌 Example Results

## Results

| Prediction Setting            | CNN  | ResNet |
|------------------------------|------|-----------|
| Multi-Frame Prediction        | 0.73 | 0.71      |
| Recursive Prediction in Testing | 0.49 | 0.64      |
| Scheduled Processing in Training | 0.50 | 0.78      |


*Note:* Actual results may vary depending on training epochs, model capacity, and hyperparameters.

---


© 2025 Anushka Chaubey / IIT Madras
