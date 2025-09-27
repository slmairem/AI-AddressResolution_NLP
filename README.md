# TEKNOFEST 2025 Hepsiburada AI-Supported Address Resolution Hackathon

## Project Overview
This project was developed for the Hepsiburada Address Matching / Resolution Hackathon.
- Final Result: **Ranked 17th among 255 teams**
- Best Validation Macro F1: **0.68590** <br>

The hackathon focused on standardizing and resolving raw address data in the Turkish logistics sector.
We aimed to parse noisy free-text addresses, correct inconsistencies, and classify them into structured, accurate, and deduplicated records.

---

## Approach
### **1. Data Cleaning & Preprocessing**  
- Normalized Turkish-specific characters (**deasciification**)  
- Regex-based cleanup of punctuation & spacing  
- Abbreviation normalization (e.g., `mah.` → `mahalle`) with **RapidFuzz**  
- Extracted **city, district, neighborhood** features from [Türkiye Adresler JSON](https://github.com/metinyildirimnet/turkiye-adresler-json)  
---
### **2. Data Augmentation**  
- Random abbreviation replacements (`mah`, `mh`, `mahalle`)  
- Character-level noise (insertion, deletion, swapping)  
- Doubled dataset size with synthetic address variations
---
### **3. Model Architecture (Hybrid BiLSTM + Attention + CNN)**  
A custom deep learning model combining sequence and convolutional networks:  

-  **Embedding Layer** – dense vector representations  
-  **BiLSTM** – captures sequential dependencies  
-  **Multi-Head Attention** – contextual token relationships  
-  **CNNs (3/4/5-grams)** – extract local n-gram features  
-  **Geographical Features** – city/district/neighborhood flags integrated  
-  **Dense + Dropout** layers – robust classification
  
**Loss:** Focal Loss (handles class imbalance)  
**Optimizer:** Adam (lr = 5e-4)  

---
### **4. Training Strategy**  
-  Early stopping & learning rate scheduling  
-  Custom callback: Macro F1 score after each epoch  
-  Automated CSV submission generation  
---
### **5. Ensemble & Post-processing**  
To boost leaderboard scores:  

- **Majority Voting** across multiple saved models (`epoch_60`, `epoch_70`, `epoch_80`, `epoch_120`, …)  
- **Tie-breaking priority order** ensures consistency  
- Final submission generated from ensemble results  
