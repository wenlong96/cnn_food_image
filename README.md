# Nutri-Grade Food Classification System (LeNet, VGG, ResNet, EfficientNet, ViT against vanilla CNN for food image labelling)

## 1. Motivation & Description
In recent years, the Singapore government introduced the Nutri-Grade system to classify beverages into four categories (A to D) based on healthiness. However, an equivalent classification system for food items has yet to be established.

This project aims to bridge that gap by developing a deep learning model that assesses the healthiness of food, supporting individuals and professionals in making informed dietary choices. Our system allows users to upload images of meals and receive instant statistics on their Nutri-Grade classifications

---

## 2. Dataset
The dataset was collected from **FoodLG**, a repository dedicated to Singaporean food.

* **Categories:** 78 food categories selected (e.g., Chicken Rice, Ban Mian, Ice Kacang).
* **Volume:** 500 representative images per category, totaling roughly 39,000 images, to ensure class balance.
* **Preprocessing:** Images were resized to uniform resolutions (e.g., 384x384 or 224x224) for consistency.

### Nutri-Grade Labeling
Since official standards exist only for beverages, we manually assigned Nutri-Grade labels (A, B, C, D) to food items based on nutritional density, cooking methods, and ingredient processing.

| Grade | Description | Examples |
| :--- | :--- | :--- |
| **A (Healthiest)** | High nutrient value, low fat/sugar, minimally processed. | Fruits, grilled salmon, whole oats. |
| **B** | Moderately healthy, may include some processed elements. | Ban Mian, roasted chicken, sushi. |
| **C** | Richer in calories, fats, or sugars; often processed. | Chicken rice, Mee Rebus, pineapple tarts. |
| **D (Least Healthy)** | Deep-fried, high saturated fat, or sugary. | Roti Prata, Ice Kacang, fried chicken. |

---

## 3. Methodology
We implemented three modeling strategies to compare performance:
1.  **78-Class Model:** Classifies images into 78 specific food categories.
2.  **Hierarchical Model:** Predicts 78 categories first, then maps them to 4 Nutri-Grades via an additional layer.
3.  **Direct 4-Class Model:** Directly predicts the Nutri-Grade (A-D) from the input image.

### Architectures Explored
We evaluated a range of deep learning architectures, from simple CNNs to Transformers:
* **Vanilla CNN & LeNet-5:** Baseline models to establish benchmarks.
* **VGG-16:** A deep CNN used to capture complex features, initialized with ImageNet weights.
* **ResNet-18:** Utilizes residual connections to mitigate vanishing gradients.
* **EfficientNet-B0:** Uses compound scaling and mobile inverted bottleneck blocks for efficient feature extraction.
* **Vision Transformer (ViT):** Applied self-attention mechanisms, treating images as sequences of patches.

---

## 4. Experimental Results
EfficientNet-B0 demonstrated the best performance, while ViT suffered from overfitting due to the dataset size.

### Performance Summary (Test Accuracy)

| Model | Direct Nutri-Grade (4-Class) | Hierarchical (78 -> 4) | Fine-Grained (78-Class) |
| :--- | :--- | :--- | :--- |
| **EfficientNet-B0** | **82.78%** | 82.42% | 77.65% |
| **VGG-16** | 75.95% | 77.76% | 50.10% |
| **ViT (Improved)** | 54.48% | 63.91% | 45.15% |
| **ResNet-18** | 52.34% | 38.15% | 48.20% |
| **LeNet-5** | 46.69% | 46.12% | 15.90% |
| **Vanilla CNN** | 44.34% | 46.08% | 16.47% |

**Key Observations:**
* **EfficientNet Superiority:** Attributed to balanced compound scaling and transfer learning from ImageNet.
* **Hierarchical vs. Direct:** For deeper models like VGG-16, hierarchical modeling provided a slight boost by leveraging fine-grained intermediate features. For EfficientNet, direct prediction was slightly better.
* **ViT Challenges:** The Transformer model initially achieved only ~35% test accuracy on 78 classes due to severe overfitting. Freezing the backbone and reducing complexity improved Nutri-Grade accuracy to ~64%.

---

## 5. Challenges & Future Work
**Current Limitations:**
* **Fine-grained Difficulty:** Visually similar foods (e.g., Chicken Rice vs. Duck Rice) are hard to distinguish.
* **Visual Cues:** Nutritional differences (e.g., sugar content) are not always visible in static images.
* **Region Specificity:** The model is limited to Singaporean cuisine.

**Future Directions:**
* **Multi-Modality:** Integrating textual data (ingredient lists) or depth information to improve accuracy.
* **Multi-Task Learning:** Predicting calories and macronutrients alongside Nutri-Grade.
* **Dataset Expansion:** Increasing diversity and regional coverage to improve generalization.
