# Does Audio Augmentation Aid Audio Unlearning? A Comprehensive Evaluation Across Methods

### Submitted to IEEE Transactions on Audio, Speech, and Language Processing (TASLP)

---

## 🔍 Overview

Machine unlearning aims to selectively erase the influence of specific training samples or classes from a model **without full retraining**, which is often computationally expensive.  
While the field has explored unlearning methods extensively, **the impact of audio data augmentation on unlearning dynamics has remained unstudied** — until now.

This work provides the **first large-scale, multi-model, multi-method investigation** of how standard audio augmentations affect both unlearning performance and collateral damage on retained data.

---

## 📌 Key Contributions

- **First comprehensive study** of the interaction between **audio data augmentation** and **machine unlearning**.
- Evaluated **9 state-of-the-art unlearning methods** across **6 augmentations**, **4 datasets**, and **6 evaluation metrics**.
- Investigated **3 modern audio architectures** in the full augmentation study:  
  - **AST-Small**  
  - **AudioMamba-Tiny**  
  - **ResNet-18**  
- Provide **baseline unlearning benchmarks** (no augmentation) for **8 total models**, including:  
  - AST {Tiny, Small, Base}  
  - AudioMamba {Tiny, Small}  
  - ResNet {18, 34, 50}  
- Conducted **entropy-based analysis** showing that augmentations systematically shift model confidence on retain vs. forget sets in predictable ways.
- Released the **largest open benchmark** for audio unlearning to date.

---

## 🧪 Experimental Setup

### **Models**
Full augmentation study:
- `AST-Small`
- `AudioMamba-Tiny`
- `ResNet18`

Baseline-only benchmarks (no data augmentation):
- `AST-Tiny`, `AST-Base`
- `AudioMamba-Small`
- `ResNet34`, `ResNet50`

---

### **Datasets (4 total)**
- **ESC-10**
- **SpeechCommands**
- **GTZAN**
- **UrbanSound8K**

---

### **Unlearning Methods (9 total)**
1. Amnesiac Unlearning  
2. Bad Teacher  
3. Boundary Unlearning  
4. UNSIR  
5. SSD  
6. SCRUB  
7. Retrain (Gold Standard)  
8. Gradient Ascent  
9. Fisher Forgetting  

---

### **Audio Augmentations (6 total)**
Used only for the TASLP 3-model detailed study:
- No augmentation  
- Time masking  
- Frequency masking  
- Additive Gaussian noise  
- Noise + Frequency masking  
- Time stretching  

---

### **Evaluation Metrics (6 total)**
1. Unlearning accuracy  
2. Retain-set accuracy  
3. Test accuracy (retain classes)  
4. Membership Inference Attack (MIA) success rate  
5. Runtime efficiency  
6. Average performance gap vs. full retraining (gold standard)

---

## 📊 Results Summary (High-Level)

- Augmentations **reduce entropy** of the output distribution on *retain* and *test* sets → models become **more confident**.  
- Entropy on *forget* sets **increases**, indicating **higher uncertainty and stronger forgetting behavior**.  
- Some unlearning methods (e.g., UNSIR, SSD) show **sensitivity to augmentation**, while others (e.g., Fisher, Bad Teacher) remain relatively stable.  
- AST-Small generally achieves **better robustness–forgetting balance**, while AudioMamba-Tiny shows **higher sensitivity** to augmentation noise.

Detailed plots & tables are available inside the `results/` directory.

---

## 🧩 Ablation Studies

### **Entropy Shift Analysis**
We compute Shannon entropy of softmax outputs across:
- Forget set  
- Retain set  
- Test set  

Data augmentation consistently:
- **Lowers entropy** on retain/test → stronger class certainty  
- **Raises entropy** on forget samples → better unlearning response  

This supports our claim that augmentations reshape the model’s confidence landscape in a way that improves selective forgetting **without retraining**.

---

## 🗂 Repository Structure (Planned)

