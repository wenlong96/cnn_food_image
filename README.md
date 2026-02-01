# Comparing LeNet, VGG, ResNet, EfficientNet, ViT against vanilla CNN for food image labelling

# Nutri-Grade Food Classification System

## 1. Motivation & Description
[cite_start]In recent years, the Singapore government introduced the Nutri-Grade system to classify beverages into four categories (A to D) based on healthiness[cite: 8]. [cite_start]However, an equivalent classification system for food items has yet to be established[cite: 9].

[cite_start]This project aims to bridge that gap by developing a deep learning model that assesses the healthiness of food, supporting individuals and professionals in making informed dietary choices[cite: 10, 13]. [cite_start]Our system allows users to upload images of meals and receive instant statistics on their Nutri-Grade classifications[cite: 12].

**Team Members:**
* [cite_start]GUO AI [cite: 3]
* [cite_start]LIM WEN LONG [cite: 4]
* [cite_start]XU FANGZHOU [cite: 5]
* [cite_start]ZHANG YIPING [cite: 6]

---

## 2. Dataset
[cite_start]The dataset was collected from **FoodLG**, a repository dedicated to Singaporean food[cite: 63].

* [cite_start]**Categories:** 78 food categories selected (e.g., Chicken Rice, Ban Mian, Ice Kacang)[cite: 72, 76].
* [cite_start]**Volume:** 500 representative images per category, totaling roughly 39,000 images, to ensure class balance[cite: 72].
* [cite_start]**Preprocessing:** Images were resized to uniform resolutions (e.g., $384 \times 384$ or $224 \times 224$) for consistency[cite: 74, 188].

### Nutri-Grade Labeling
[cite_start]Since official standards exist only for beverages, we manually assigned Nutri-Grade labels (A, B, C, D) to food items based on nutritional density, cooking methods, and ingredient processing[cite: 65, 66].

| Grade | Description | Examples |
| :--- | :--- | :--- |
| **A (Healthiest)** | High nutrient value, low fat/sugar, minimally processed. | [cite_start]Fruits, grilled salmon, whole oats[cite: 68]. |
| **B** | Moderately healthy, may include some processed elements. | [cite_start]Ban Mian, roasted chicken, sushi[cite: 69]. |
| **C** | Richer in calories, fats, or sugars; often processed. | [cite_start]Chicken rice, Mee Rebus, pineapple tarts[cite: 70]. |
| **D (Least Healthy)** | Deep-fried, high saturated fat, or sugary. | [cite_start]Roti Prata, Ice Kacang, fried chicken[cite: 71]. |

---

## 3. Methodology
[cite_start]We implemented three modeling strategies to compare performance[cite: 175]:
1.  **78-Class Model:** Classifies images into 78 specific food categories.
2.  **Hierarchical Model:** Predicts 78 categories first, then maps them to 4 Nutri-Grades via an additional layer.
3.  **Direct 4-Class Model:** Directly predicts the Nutri-Grade (A-D) from the input image.

### Architectures Explored
We evaluated a range of deep learning architectures, from simple CNNs to Transformers:
* [cite_start]**Vanilla CNN & LeNet-5:** Baseline models to establish benchmarks[cite: 183, 199].
* [cite_start]**VGG-16:** A deep CNN used to capture complex features, initialized with ImageNet weights[cite: 216, 218].
* [cite_start]**ResNet-18:** Utilizes residual connections to mitigate vanishing gradients[cite: 237].
* [cite_start]**EfficientNet-B0:** Uses compound scaling and mobile inverted bottleneck blocks for efficient feature extraction[cite: 269, 420].
* [cite_start]**Vision Transformer (ViT):** Applied self-attention mechanisms, treating images as sequences of patches[cite: 306, 307].

---

## 4. Experimental Results
[cite_start]EfficientNet-B0 demonstrated the best performance, while ViT suffered from overfitting due to the dataset size[cite: 414, 438].

### Performance Summary (Test Accuracy)

| Model | Direct Nutri-Grade (4-Class) | Hierarchical (78 $\to$ 4) | Fine-Grained (78-Class) |
| :--- | :--- | :--- | :--- |
| **EfficientNet-B0** | [cite_start]**82.78%** [cite: 302] | [cite_start]82.42% [cite: 302] | [cite_start]77.65% [cite: 302] |
| **VGG-16** | [cite_start]75.95% [cite: 226] | [cite_start]77.76% [cite: 226] | [cite_start]50.10% [cite: 226] |
| **ViT (Improved)** | [cite_start]54.48% [cite: 394] | [cite_start]63.91% [cite: 394] | [cite_start]45.15% [cite: 394] |
| **ResNet-18** | [cite_start]52.34% [cite: 259] | [cite_start]38.15% [cite: 259] | [cite_start]48.20% [cite: 259] |
| **LeNet-5** | [cite_start]46.69% [cite: 207] | [cite_start]46.12% [cite: 207] | [cite_start]15.90% [cite: 207] |
| **Vanilla CNN** | [cite_start]44.34% [cite: 191] | [cite_start]46.08% [cite: 191] | [cite_start]16.47% [cite: 191] |

**Key Observations:**
* [cite_start]**EfficientNet Superiority:** Attributed to balanced compound scaling and transfer learning from ImageNet[cite: 416, 424].
* [cite_start]**Hierarchical vs. Direct:** For deeper models like VGG-16, hierarchical modeling provided a slight boost by leveraging fine-grained intermediate features[cite: 233]. [cite_start]For EfficientNet, direct prediction was slightly better[cite: 302].
* [cite_start]**ViT Challenges:** The Transformer model initially achieved only ~35% test accuracy on 78 classes due to severe overfitting[cite: 346]. [cite_start]Freezing the backbone and reducing complexity improved Nutri-Grade accuracy to ~64%[cite: 394, 412].

---

## 5. Challenges & Future Work
**Current Limitations:**
* [cite_start]**Fine-grained Difficulty:** Visually similar foods (e.g., Chicken Rice vs. Duck Rice) are hard to distinguish[cite: 135, 444].
* [cite_start]**Visual Cues:** Nutritional differences (e.g., sugar content) are not always visible in static images[cite: 445].
* [cite_start]**Region Specificity:** The model is limited to Singaporean cuisine[cite: 446].

**Future Directions:**
* [cite_start]**Multi-Modality:** Integrating textual data (ingredient lists) or depth information to improve accuracy[cite: 450].
* [cite_start]**Multi-Task Learning:** Predicting calories and macronutrients alongside Nutri-Grade[cite: 451].
* [cite_start]**Dataset Expansion:** Increasing diversity and regional coverage to improve generalization[cite: 448].
