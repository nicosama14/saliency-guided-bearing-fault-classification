# saliency-guided-bearing-fault-classification

Explainable bearing fault classification using CNN saliency maps, XAI-guided frequency band extraction, and interpretable logistic regression.

This repository contains the implementation of the paper:

\*\*Interpretable Bearing Fault Classification via Saliency-Guided Feature Extraction from CNNs\*\*

The project proposes an explainable AI framework for vibration-based bearing fault diagnosis. Instead of using explainability only for visualization, the framework uses Grad-CAM and Grad-CAM++ saliency maps to identify relevant time-frequency regions, extract physically meaningful frequency bands, and train a compact interpretable classifier.

## Overview

Deep learning models, especially convolutional neural networks, can achieve high accuracy in bearing fault diagnosis when trained on time-frequency representations such as STFT spectrograms and CWT scalograms. However, these models are often difficult to interpret, which limits their acceptance in practical predictive maintenance applications.

This project addresses that limitation by connecting CNN-based classification with transparent feature extraction. A lightweight CNN is first trained on time-frequency images. Then, Grad-CAM and Grad-CAM++ are applied to identify the frequency regions that contribute most to the CNN decisions. These regions are converted into saliency-guided frequency bands, from which statistical features are extracted. Finally, a multinomial logistic regression model is trained using these features, providing a simpler and interpretable diagnostic model.

## Main Features

- Bearing fault classification using vibration signals
- Leakage-safe signal segmentation
- STFT and CWT time-frequency image generation
- Lightweight CNN training
- Grad-CAM and Grad-CAM++ saliency analysis
- Saliency faithfulness evaluation using deletion and insertion metrics
- Saliency stability evaluation using Spearman correlation and IoU
- Targeted PGD adversarial sensitivity analysis
- XAI-guided frequency band extraction
- Statistical feature extraction from selected frequency bands
- Interpretable multinomial logistic regression classification
- Feature importance analysis using permutation importance

## Methodology

The general workflow is:

1. **Signal segmentation**
Vibration signals are divided into fixed-length windows using a leakage-safe splitting strategy.

2. **Time-frequency image generation**  
Each segment is transformed into STFT and CWT representations.

3. **CNN training**  
Lightweight CNN models are trained for four-class bearing fault classification.

4. **Saliency analysis**  
Grad-CAM and Grad-CAM++ are used to identify the time-frequency regions that contribute to the CNN decisions.

5. **Robustness and faithfulness evaluation**  
Saliency maps are evaluated using deletion/insertion curves, adversarial perturbations, and stability metrics.

6. **Frequency band extraction**  
Class-wise saliency maps are aggregated to obtain frequency saliency curves. A threshold is applied to select the most relevant frequency bands.

7. **Interpretable feature extraction**  
Statistical features are extracted from the selected frequency bands.

8. **Logistic regression classification**  
A transparent linear classifier is trained using the saliency-derived features.

## Dataset

The experiments are conducted using the Case Western Reserve University (CWRU) bearing vibration dataset.

The classification task includes four bearing conditions:

- Baseline
- Inner race fault
- Outer race fault
- Ball fault

The raw dataset is not included in this repository due to size and licensing considerations. Users should download the dataset from the official CWRU Bearing Data Center and organize it locally before running the scripts.

## Time-Frequency Representations

Two time-frequency representations are considered:

| Representation | Description |

| STFT | Short-Time Fourier Transform spectrograms |

| CWT | Continuous Wavelet Transform scalograms |

Both representations preserve physically meaningful time and frequency axes, which allows saliency maps to be interpreted in terms of vibration frequency regions.

## CNN Architecture

The project uses a compact 2D CNN inspired by interpretable bearing fault diagnosis literature. The model receives a `256 × 256` RGB time-frequency image and outputs four class probabilities.

The architecture includes:

- Convolutional layers
- ReLU activations
- Max-pooling layers
- Fully connected layers
- Softmax classification output

The network is intentionally lightweight to support interpretability and avoid unnecessary model complexity.

## Explainability Analysis

The project applies:
- Grad-CAM
- Grad-CAM++
- Deletion and insertion faithfulness metrics
- Spearman rank correlation
- IoU@20% stability metric
- Targeted PGD adversarial attacks

The goal is to evaluate whether the saliency maps highlight meaningful and stable time-frequency regions.

## Saliency-Guided Feature Extraction

After generating saliency maps, frequency saliency curves are obtained by aggregating saliency values over the time axis. A threshold is applied to identify important frequency bands.

For each selected band, statistical features are extracted, including:

- Mean
- Variance
- RMS
- Skewness
- Kurtosis

These features provide a compact and physically interpretable representation of the vibration signal.

## Interpretable Classifier

A multinomial logistic regression model is trained using the saliency-guided features.

Unlike the CNN, the logistic regression model provides transparent linear decision boundaries. The contribution of each feature can be inspected directly, allowing the final classification decision to be traced back to specific frequency bands and statistical descriptors.

## Main Results

The experiments show that:

- CNNs trained on STFT and CWT images achieve high classification accuracy.
- Grad-CAM produces stable and physically meaningful saliency regions.
- Saliency-guided frequency bands preserve discriminative fault information.
- A logistic regression model trained on Grad-CAM-derived features achieves performance close to the CNN.
- Grad-CAM-derived features outperform Grad-CAM++-derived features in the interpretable classification stage.
- Higher-order statistics such as skewness and kurtosis are among the most important features.
- The saliency threshold strongly affects the final classification performance.

## Notes

Large raw datasets, generated image datasets, trained model checkpoints, and intermediate outputs are not included in this repository.

This repository is intended to provide the implementation, selected results, and documentation for reproducibility and research portfolio purposes.

## Citation

If you use this code or methodology, please cite the related paper:

N. Salguero España, M. Mohandes, and A. Al-Shaikhi, "Interpretable Bearing Fault Classification via Saliency-Guided Feature Extraction from CNNs."

## Author
Nicolás Salguero España
M.S. Student in Electrical Engineering
King Fahd University of Petroleum and Minerals


