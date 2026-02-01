# Comparing LeNet, VGG, ResNet, EfficientNet, ViT against vanilla CNN for food image labelling

# Nutri-Grade Food Classification System

## 1. Overview

This project implements a deep learning-based system to classify Singaporean food items into **78 fine-grained categories** and subsequently predict their **Nutri-Grade (A, B, C, D)**. Designed to help users monitor their diet, the system addresses the gap in Nutri-Grade classification for food items (currently only available for beverages in Singapore).

The system explores multiple architectures, including **Vanilla CNN, LeNet-5, VGG-16, ResNet-18, EfficientNet-B0, and Vision Transformers (ViT)**, comparing their performance on a locally curated dataset.

---

## 2. Dataset

* 
**Source:** Images were collected from **FoodLG**, a repository of Singaporean food.


* 
**Size:** The dataset consists of **500 images per category** across **78 categories**, ensuring class balance.


* 
**Preprocessing:** All images were resized to **384x384** (or 224x224 for specific models) to ensure consistency.


* 
**Labeling:** Nutri-Grade labels (A, B, C, D) were manually assigned based on nutritional density, processing level, and cooking methods.


* 
**Grade A:** High nutrient density, minimal processing (e.g., fruits, grilled salmon).


* 
**Grade B:** Moderately healthy (e.g., Ban Mian, roasted chicken).


* 
**Grade C:** Higher calorie/fat/sugar content (e.g., Chicken Rice, Mee Rebus).


* 
**Grade D:** Deep-fried or high sugar/fat (e.g., Roti Prata, Ice Kacang).





---

## 3. Models & Architectures

We implemented three variants for each architecture to test different prediction strategies:

1. 
**78-Class Model:** Classifies images into 78 food categories.


2. 
**Hierarchical Model:** Classifies into 78 categories first, then maps them to 4 Nutri-Grades via an additional layer.


3. 
**Direct 4-Class Model:** Directly predicts the Nutri-Grade from the image.



### Key Models Tested:

* **EfficientNet-B0:** The top-performing model. It utilizes compound scaling and mobile inverted bottleneck convolutions, making it highly effective for fine-grained feature extraction.


* 
**Vision Transformer (ViT):** Utilizes self-attention but suffered from overfitting on this dataset due to its lack of inductive bias and the dataset size.


* **ResNet-18:** A residual network trained from scratch. It performed decently but lacked the fine-grained capabilities of EfficientNet.


* 
**VGG-16:** A deep CNN that showed strong performance but was computationally heavier than EfficientNet.



---

## 4. Performance Summary

| Model | Task | Test Accuracy | Observations |
| --- | --- | --- | --- |
| **EfficientNet-B0** | Nutri-Grade (Direct) | **82.78%** | Best overall performance.

 |
| **EfficientNet-B0** | Nutri-Grade (Hierarchical) | 82.42% | Very close to direct prediction.

 |
| **EfficientNet-B0** | 78-Class Classification | 77.65% | High accuracy for fine-grained task.

 |
| **ViT (Optimized)** | Nutri-Grade (Hierarchical) | 63.91% | Improved after freezing backbone, but still overfit.

 |
| **ResNet-18** | Nutri-Grade (Direct) | 52.34% | Moderate performance; benefitted from direct prediction.

 |
| **Vanilla CNN** | Nutri-Grade (Hierarchical) | 46.08% | Too shallow for complex feature extraction.

 |

**Key Finding:** EfficientNet-B0 significantly outperformed other models due to its ability to capture fine-grained features (texture, color) essential for distinguishing similar food items.

---

## 5. Usage

To train the models, ensure you have the necessary dependencies installed. The project creates wrappers for different model architectures to switch between 78-class and 4-class prediction easily.

### Prerequisites

* Python 3.x
* PyTorch
* Torchvision
* Scikit-learn (for metrics)

### Training

Models are trained using standard PyTorch loops with:

* 
**Loss Function:** CrossEntropyLoss.


* 
**Optimizer:** Adam or AdamW.


* 
**Regularization:** Early stopping, Dropout, and Batch Normalization were employed to mitigate overfitting.



---

## 6. Challenges & Future Work

* 
**Visual Similarity:** Distinguishing between visually similar categories (e.g., "Chicken Rice" vs. "Duck Rice") remains difficult.


* **Dataset Limitations:** The dataset is region-specific (Singaporean food). Future work could expand to other cuisines.


* 
**Multi-Modality:** Integrating text data (ingredients) or depth estimation could improve accuracy for complex dishes.



---

## 7. Credits

* 
**Project Team:** GUO AI, LIM WEN LONG, XU FANGZHOU, ZHANG YIPING.


* 
**References:** See the project report for a full list of citations, including works on Nutrition5k and FoodLG.
