
# Video Frame Prediction using Deep Learning on Moving MNIST

This project implements and evaluates a deep learning model for video prediction, specifically forecasting future frames in a Moving MNIST sequence. The primary objective is to explore how convolutional and recurrent architectures can learn spatiotemporal patterns for accurate short-term video forecasting.

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

- **Dataset:** Moving MNIST — a synthetic dataset of MNIST digits moving inside a frame.

- **Task:** Predict 5 future frames given 10 input frames.

- **Model Architecture:**
  - Encoder-Decoder style convolutional model with ConvLSTM layers.
  - Trained using Mean Squared Error (MSE) loss.
  - Evaluated using Structural Similarity Index (SSIM) for perceptual similarity.

- **Evaluation:**
  - Average SSIM computed across predicted frames.
  - Frame-wise prediction accuracy assessed against ground-truth frames.

---

## 🔍 Key Features

- Handles sequential video frame prediction using ConvLSTM layers.
- SSIM-based evaluation pipeline integrated for perceptual quality assessment.
- Modular and extensible architecture suitable for other video datasets (e.g., KTH Actions, UCF101).

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

3. **Run the Notebook**
   Open and run `EA_VideoPrediction_MNIST.ipynb` using Jupyter Notebook or VS Code. The notebook is fully self-contained.

---

## 📊 Metrics

- **SSIM (Structural Similarity Index):**
  - Computed per predicted frame.
  - Averaged over the 5-frame prediction horizon.
  - Measures perceptual similarity between predicted and ground-truth frames.

---

## 📌 Example Results

| Metric              | Value            |
|---------------------|------------------|
| Average SSIM (5 frames) | ~0.75 (example) |

*Note:* Actual results may vary depending on training epochs, model capacity, and hyperparameters.

---

Feel free to open issues or submit pull requests for improvements and feature requests!

---

© 2025 Your Name / Your Organization
