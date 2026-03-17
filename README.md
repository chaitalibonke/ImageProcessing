# ImageProcessing
This code processes a lung CT image by analyzing it in the frequency domain using Fast Fourier Transform(FFT), downsampling it, and reconstructing it using FFT-based and bilinear interpolation. It compares reconstruction quality using MSE, showing bilinear interpolation preserves the image far better than the FFT approach.

# Lung CT Image Processing: FFT vs Interpolation

## Overview
This project explores image processing techniques applied to a lung CT scan using 
both frequency-domain (FFT) and spatial-domain interpolation methods. The goal is 
to analyze how image quality is affected by downsampling and reconstruction.

---

## Objective
- Analyze an image in the spatial vs. frequency domain
- Study the impact of downsampling on image quality
- Reconstruct images using:
  - FFT-based interpolation (zero-padding in frequency domain)
  - Bilinear interpolation (spatial domain baseline)
- Compare reconstruction quality using Mean Squared Error (MSE)

---

## Dataset
- **Image:** `lung_ct.jpg`
- **Type:** Grayscale lung CT scan
- **Use Case:** Medical imaging — structure and detail preservation are critical

---

## Methodology

### 1. Image Preprocessing
- Load the image and convert to grayscale
- Visualize and inspect spatial dimensions

### 2. Frequency Analysis (FFT)
- Apply 2D Fast Fourier Transform (FFT)
- Extract magnitude spectrum and phase
- Use `fftshift` for centered frequency visualization

### 3. Downsampling
- Reduce image resolution by 50%
- Simulates realistic information loss

### 4. FFT-Based Reconstruction
- Transform the downsampled image to the frequency domain
- Apply zero-padding to restore original dimensions
- Reconstruct using Inverse FFT (IFFT)

### 5. Bilinear Interpolation
- Resize the downsampled image using spatial bilinear interpolation
- Serves as the standard baseline for comparison

### 6. Evaluation
- Compare each reconstructed image against the original
- Metric: Mean Squared Error (MSE) — lower is better

---

## Results

| Method                  | MSE       |
|-------------------------|-----------|
| FFT-Based Interpolation | 31734.20  |
| Bilinear Interpolation  |    18.43  |

### Key Findings
- **Bilinear interpolation significantly outperforms FFT-based reconstruction** 
  in this task, achieving an MSE of 18.43 vs. 31734.20.
- The high MSE of the FFT method is expected: naive zero-padding in the frequency 
  domain introduces ringing artifacts (Gibbs phenomenon) and does not recover 
  lost high-frequency detail.
- FFT remains a powerful tool for **frequency analysis and filtering**, but 
  requires advanced techniques (e.g., windowing, regularization) to be 
  competitive for image reconstruction.
- For medical imaging tasks where structural fidelity is critical, 
  **spatial interpolation methods are the more reliable choice**.

---

## Tech Stack
- Python
- NumPy
- Matplotlib
- Pillow (PIL)
- Scikit Learn

---

## How to Run

Install dependencies:
```bash
pip install numpy pandas matplotlib pillow scipy scikit-learn
```

Run the script:
```bash
python lung_ct_processing.py
```

> Replace `lung_ct_processing.py` with the name of your actual script file.

---

## Conclusion
This project demonstrates that simpler spatial interpolation methods can 
outperform frequency-domain approaches in image reconstruction tasks. 
While FFT is invaluable for spectral analysis, bilinear interpolation 
preserves structural integrity more effectively when upscaling a 
downsampled medical image. Choosing the right technique depends on the 
goal — analysis vs. reconstruction.


