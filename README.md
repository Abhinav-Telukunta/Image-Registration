# Image Registration Using VoxelMorph

## Project Description
This project implements image registration using the VoxelMorph framework. Image registration aligns a moving image with a fixed image, which is crucial in medical imaging applications like tracking anatomical changes and fusing multi-modal images. The project leverages the VoxelMorph image registration network with two loss functions: Normalized Cross-Correlation (NCC) and Sum of Squared Differences (SSD).

## Purpose
The main goals of this project are:
1. To perform 3D image registration for medical images.
2. To compare the performance of the VoxelMorph model using NCC and SSD loss functions.
3. To evaluate the improvement in registration quality using metrics like the Dice coefficient and Hausdorff distance.

## Dataset
The dataset consists of 3D medical images and their segmentations in NIfTI format. The training and testing sets contain images of uniform dimensions `(160, 192, 224)` with voxel spacing of `1mm x 1mm x 1mm`.

## Methods
1. **Data Preparation**:
   - Images and their segmentations were loaded and preprocessed.
   - Pairs of moving and fixed images were generated for training and testing.
   - Custom data generators were implemented for batch processing.

2. **VoxelMorph Network**:
   - The VoxelMorph Dense model was used for registration with a dense deformation field.
   - Loss functions included:
     - NCC: Measures similarity between the fixed and moving images.
     - SSD: Measures the squared differences between the fixed and moving images.
   - Gradient loss was added to ensure smoothness of the deformation field.
   - Training used the Adam optimizer with a learning rate of `1e-4` and regularization parameter `λ = 0.05`.

3. **Evaluation Metrics**:
   - **Dice Coefficient**: Measures overlap between the registered segmentation and the ground truth.
   - **Hausdorff Distance**: Measures the maximum distance between the edges of the registered segmentation and the ground truth.

## Results
1. **NCC Loss**:
   - **Dice Coefficient**:
     - Before Registration: `0.5727`
     - After Registration: `0.7307`
   - **Hausdorff Distance**:
     - Before Registration: `8.4378 mm`
     - After Registration: `8.9803 mm`
   
2. **SSD Loss**:
   - **Dice Coefficient**:
     - Before Registration: `0.5727`
     - After Registration: `0.7231`
   - **Hausdorff Distance**:
     - Before Registration: `8.4378 mm`
     - After Registration: `9.4424 mm`

3. Visualizations:
   - Significant improvement in the overlap of registered segmentations, as observed in Dice coefficient plots.
   - Slight increase in Hausdorff distance for both loss functions, likely due to outlier pixels.

## Conclusion
The VoxelMorph model demonstrates effective image registration, with NCC performing slightly better than SSD in terms of Dice coefficient. While Hausdorff distance results showed unexpected increases due to stray pixels, the overall alignment and segmentation overlap significantly improved. This project highlights the potential of deep learning-based approaches for robust and efficient medical image registration.

