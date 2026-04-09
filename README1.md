Overview

This project involves a Convolutional Neural Network (CNN) designed to analyze chest X-ray images and determine whether a patient has pneumonia. The primary objective was to maximize the detection of pneumonia cases.

Project Description

In this work, a CNN model was trained on chest X-ray images to classify them into two categories: NORMAL or PNEUMONIA. The main focus was on achieving high recall to ensure that as many pneumonia cases as possible were correctly identified.

Dataset
Training Set: 1,341 normal | 3,875 pneumonia
Validation Set: 8 normal | 8 pneumonia
Test Set: 234 normal | 390 pneumonia

The dataset exhibits significant class imbalance, with nearly three times more pneumonia images than normal ones, requiring careful handling during training.

Methodology

1. Data Preparation
The dataset was loaded by mounting Google Drive, organizing directory paths, and verifying the number of images in each class.

2. Handling Class Imbalance
Class weights were computed to emphasize the minority class (NORMAL), ensuring the model does not become biased toward predicting pneumonia.

3. Preprocessing and Augmentation
All images were normalized to a [0,1] range. Light data augmentation was applied only to the training set.

4. Model Construction
A CNN architecture with four convolutional blocks (32 → 64 → 128 → 256 filters) was developed, followed by dense layers.

5. Model Compilation
The model was compiled using the Adam optimizer and binary crossentropy loss. Performance metrics included accuracy, precision, recall, AUC, and F1-score.

6. Callbacks Setup
Early stopping, model checkpointing, and learning rate reduction were implemented, all monitored using validation recall.

7. Training
The model was trained for up to 30 epochs with class weights applied.

8. Evaluation
Performance was assessed on the test set using metrics such as confusion matrix, ROC AUC, sensitivity, and specificity.

Approach
Handling Class Imbalance

Class imbalance was addressed using computed class weights. The NORMAL class was assigned approximately 1.94× more weight than the pneumonia class to prevent biased predictions.

Data Augmentation
Small rotations (±15°)
Minor horizontal and vertical shifts
Slight zoom and shear
Horizontal flipping

Augmentation was kept minimal to maintain clinical realism.

Model Architecture
Four convolutional blocks with filters: 32 → 64 → 128 → 256
Each block includes Batch Normalization, MaxPooling, and 25% Dropout
GlobalAveragePooling2D used instead of flattening to reduce parameters and overfitting
Two dense layers (256 and 128 units) with L2 regularization and 50% Dropout
Tanh activation used instead of ReLU to retain negative values
Output layer: single neuron with sigmoid activation for binary classification
Training Configuration
Optimizer: Adam (learning rate = 0.001)
Loss Function: Binary crossentropy
Callbacks: Early stopping and checkpointing based on validation recall
Learning Rate Scheduling: Reduced when validation loss stagnates
Priority Metric: Recall, to minimize missed pneumonia cases
Libraries Used
TensorFlow / Keras — model development and training
NumPy — numerical operations
Pandas — data handling

| Metric               | Score |
| -------------------- | ----- |
| Accuracy             | 62.5% |
| Recall (Sensitivity) | 100%  |
| Specificity          | 0%    |
| AUC                  | 0.72  |
| F1 Score             | 0.63  |

The model classified every image as PNEUMONIA. While it successfully detected all 390 pneumonia cases (no false negatives), it incorrectly labeled all 234 healthy cases as pneumonia (no true negatives).

This behavior resulted from strong emphasis on recall due to class weighting and monitoring validation recall. Essentially, the model adopted a trivial strategy: always predicting pneumonia to avoid missing any cases.

However, the ROC AUC score of 0.72 indicates that the model’s probability outputs still contain useful discriminatory information. Adjusting the classification threshold could potentially improve balance between sensitivity and specificity.

Limitations
The validation set contains only 16 images, making performance evaluation unreliable. A single misclassification significantly affects metrics.
The model collapsed into predicting only one class (PNEUMONIA), which limits its practical usefulness.

OpenCV & PIL — image preprocessing
Matplotlib & Seaborn — visualization
Scikit-learn — class weights and evaluation metrics
