# Deepfake Detection using AI Techniques

A deep learning model that classifies face images as Real or Fake (AI-generated/deepfake), built using EfficientNet-B0 with transfer learning.

## Project Overview
This project applies cybersecurity and AI techniques to detect manipulated facial images — a growing threat in digital identity verification, misinformation, and fraud.

## Dataset
[140k Real and Fake Faces](https://www.kaggle.com/datasets/xhlulu/140k-real-and-fake-faces) — Kaggle

## Model
- **Architecture:** EfficientNet-B0 (pretrained on ImageNet)
- **Framework:** PyTorch + timm
- **Training:** 3 epochs, Adam optimizer (lr=1e-4), Colab T4 GPU
- **Input:** 224x224 RGB face images, normalized

## Results
- **Test Accuracy:** 59%
- **F1-Score:** Fake = 0.55, Real = 0.61

### Key Finding
A gap between training accuracy (95.7%) and test accuracy (59%) indicates **overfitting** — the model memorized training patterns rather than learning generalizable deepfake artifacts. This is a well-documented challenge in deepfake detection research due to the high visual similarity between modern GAN-generated faces and real ones.

### Security Implication
The confusion matrix showed **70 false negatives** (fake faces misclassified as real) — the more dangerous error type in a security context, since it means deepfakes could pass undetected.

## Explainability
Grad-CAM was used to visualize which facial regions influenced the model's decisions — typically highlighting eyes, mouth, and facial boundaries, where deepfake artifacts commonly appear.

## Demo
An interactive web demo was built using Gradio, allowing users to upload a face image and receive a Real/Fake prediction with confidence scores.

## Future Improvements
- Train on the full 140k dataset for more epochs
- Add dropout and stronger data augmentation to reduce overfitting
- Test generalization on StyleGAN-generated faces (e.g., thispersondoesnotexist.com)
- Explore XceptionNet architecture, proven effective on FaceForensics++

## Files
| File | Description |
|------|-------------|
| `deepfake_detection.ipynb` | Full training and evaluation notebook |
| `deepfake_detector.pth` | Trained model weights |
| `confusion_matrix.png` | Evaluation confusion matrix |
| `gradcam_result.png` | Grad-CAM interpretability visualization |

## Tech Stack
Python, PyTorch, timm, Gradio, Google Colab (T4 GPU)
