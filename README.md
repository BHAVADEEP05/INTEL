# Motion Deblurring using Knowledge Distillation

This project implements a lightweight CNN model for single-image motion deblurring using **knowledge distillation** from the pretrained **Restormer** model. The student model is trained on the **GoPro dataset** using supervision from both ground truth images and Restormer-generated outputs.

---

## 🔗 Download Project Files

📁 Download dataset, pretrained Restormer weights, and outputs from this Google Drive folder:  
**[Click here to access](https://drive.google.com/drive/folders/1zHJ79d4K-QQJRFZFjhL5ENrzCpgEOSQ8?usp=sharing)**  

---

## 📁 Dataset Structure

/train/blur/ # Blurred input images
/train/sharp/ # Ground truth sharp images
/teacher_outputs/ # Deblurred outputs from Restormer
<img width="656" height="551" alt="image" src="https://github.com/user-attachments/assets/a0166e0f-961a-4b65-8fde-6cfce2a489de" />



---

## 🧠 Student Model Architecture

A custom lightweight CNN:
- Conv2D(3→32) → ReLU
- Conv2D(32→64) → ReLU
- Conv2D(64→32) → ReLU
- Conv2D(32→3)

---

## 🧪 Loss Functions

- ✅ L1 Reconstruction Loss
- ✅ Knowledge Distillation Loss (student vs teacher)
- ✅ Perceptual Loss (VGG16 features)
- ✅ Edge Loss (Sobel filter-based)
- ✅ Feature Distillation Loss

---

## 🚀 How to Run

1. Clone and set up Restormer:
   ```bash
   git clone https://github.com/swz30/Restormer.git
   cd Restormer
   pip install -r requirements.txt

2. Download pretrained Restormer and generate teacher outputs:
wget https://github.com/swz30/Restormer/releases/download/v1.0/motion_deblurring.pth -P Motion_Deblurring/pretrained_models
python demo.py --task Motion_Deblurring \
  --input_dir /train/blur \
  --result_dir /teacher_outputs


## 📊 Evaluation Results

After 10 epochs of training on the GoPro dataset, the student model achieved:SSIM: ~0.87
📊 Final Loss Breakdown:

🔹 Reconstruction Loss (L1): 0.042551

🔹 Perceptual Loss (VGG): 0.653914

🔹 Feature Distillation Loss: 0.038654

🔹 Edge/Gradient Loss: 0.350876

Despite its compact design, the student model successfully restores image structure and fine texture, producing visually sharp outputs while significantly reducing computation compared to the Restormer teacher model.


