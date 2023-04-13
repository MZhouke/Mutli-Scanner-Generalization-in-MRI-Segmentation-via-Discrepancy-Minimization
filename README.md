# Mutli-Scanner-Generalization-in-MRI-Segmentation-via-Discrepancy-Minimization
The goal of this study is to improve the generalization of MRI segmentation models when dealing with data collected from different scanners. We will explore various training strategies and domain adaptation techniques to enhance the performance of the models across domains. The [`dataset`](https://brain-development.org/ixi-dataset/) used in this study consists of MRI data from three hospitals: Guys and IOP with 1.5T scanners, and HH with a 3T scanner. We create source dataset from Guys and IOP using 1.5T scanners, and target dataset from HH. The goal is to investigate generalization methods to determine the best multi-scanner generalization method. We will compare the following approaches: 

1. Direct transfer of a model trained on the source domain
2. Training a model from scratch on the target domain (very limited data)
3. Using transfer learning to fine-tune a model from the source domain to the target domain
4. Training a model on all data with intensity normalization applied. 

We aim to identify the most effective method for improving multi-scanner generalization in MRI segmentation.

In the end, we propose a novel training regularizer with combined MMD loss


Conclusion: 
1. Direct Transfer (c1) - Accuracy: 0.8054, Time per Epoch: 23 seconds

In this approach, a pre-trained model from the source dataset (388 subjects) is directly applied to the target dataset (176 subjects) without any additional training. This method is quick and requires no additional data for training but can result in reduced performance due to the domain shift.

2. Training from Scratch (c2) - Accuracy: 0.8657, Time per Epoch: 9 seconds

The model is trained entirely on the target dataset (176 subjects), disregarding any pre-trained knowledge from the source dataset. This method can be time-consuming but achieves better performance than direct transfer. However, it may require a larger target dataset for optimal results.

3. Transfer Learning (c3) - Accuracy: 0.8913, Time per Epoch: 9.5 seconds

A pre-trained model from the source dataset (388 subjects) is fine-tuned on the target dataset (176 subjects). This method combines the benefits of both direct transfer and training from scratch, achieving better performance.

4. Histogram Normalization (c4) - Accuracy: 0.9469, Time per Epoch: 25 seconds

This method involves matching the intensity distribution of the source and target datasets through histogram normalization before applying the model. It improves the performance compared to the previous methods but requires additional pre-processing steps which takes additional computational resources.

5. MMD Loss (c5) - Accuracy: 0.9581, Time per Epoch: 22 seconds

The model is trained by minimizing combined loss of dice loss and the Maximum Mean Discrepancy (MMD) loss, which measures the distance between the source and target domain feature distributions. This method achieves the highest accuracy and has comparable computation time to histogram normalization (with pre-processing).

In summary, combined loss offers the best performance with the highest accuracy and takes advantage of the combined dataset for training. It also has a similar computation time to the histogram normalization method while offering better accuracy.
