# CSC120_Laboratory-Work-4-Activity-Improving-CNN-Performance-Using-Regularization
# Google Collab Link: https://colab.research.google.com/drive/1gYt3QRySZb9R6XrNn6nOONgaBxODLrt0?usp=sharing

# GUIDE QUESTIONS: Reflection & Analysis

### A. Model Evaluation Analysis
1. **Weakest-performing classes**: Based on the final confusion matrix, **Hemlock Tree** and **Pine Tree** were the weakest, often showing high confusion with other species. **Oak Tree** also struggled with a precision of 0.48.
2. **Metric Variation**: Precision and Recall varied significantly. High-performing classes like **Pomegranate Tree** (F1 0.93) had distinct visual features, while others dropped as low as 0.47 F1-score due to visual similarities between tree leaves.
3. **Low Recall**: Indicates that the model is missing many actual instances of that class (high False Negatives). For example, it often failed to identify Pine Trees when they were actually present.
4. **AUC vs. Accuracy**: Accuracy measures the percentage of correct top-1 guesses. AUC reflects the model's ability to rank classes correctly. Our low AUC (0.51) compared to 70% accuracy indicates that while the top guess is often right, the model is 'unsure' and the probability gap between the correct and incorrect classes is very narrow.

### B. Model Improvement
5. **Data Augmentation**: It initially caused the validation accuracy to drop from 80% to 70%, but it helped the model generalize. It makes training harder but prevents the model from simply memorizing the dataset orientation.
6. **Batch Normalization**: It standardizes the inputs to each layer, which stabilizes the learning process and significantly speeds up training by allowing higher learning rates.
7. **Dropout**: It randomly 'turns off' neurons during training, forcing the network to learn redundant representations. This prevents the model from relying on a single specific pixel pattern, thus reducing overfitting.
8. **Early Stopping**: It monitored the `val_loss`. When the loss stopped improving for 10 consecutive epochs, it halted training to prevent the model from starting to memorize the training data (overfitting).

### C. Performance Comparison
9. **Improvements**: We observed more stable convergence. Although raw accuracy was lower (70% vs 80%), the 'Improved' model is less likely to fail on brand-new, unseen images due to the added regularization.
10. **Most Impactful Enhancement**: **Learning Rate Optimization** and **Dropout**. The learning rate adjustment prevented the 'model collapse' (accuracy flatlining at 5%), while Dropout ensured the training and validation curves stayed closer together.
11. **Accuracy Gap**: Yes, the gap narrowed. In the baseline, training accuracy often soared to 90%+ while validation trailed. With regularization, the two metrics tracked more closely, indicating better generalization.

### D. Explainability (Grad-CAM Integration)
12. **Grad-CAM Understanding**: It visualized the 'attention' of the CNN. It showed whether the model was looking at the actual tree/leaves or just random background noise or sky to make its decision.
13. **Relevant Regions**: The heatmaps (e.g., in Part 5/6) showed the model focusing on the central textures of the leaves. In the improved model, the heatmap was often more centered on the object rather than the edges.
14. **Importance of Explainability**: In real-world AI (like forestry or medicine), we need to know *why* a model made a choice to ensure it isn't biased or relying on 'shortcuts' (like a watermark or specific lighting) rather than the actual object features.
