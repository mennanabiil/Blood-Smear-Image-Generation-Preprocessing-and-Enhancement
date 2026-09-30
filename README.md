# Blood Smear Image Preprocessing and Enhancement

This project explores common image preprocessing techniques using a synthetic peripheral blood smear generated in Python. The goal is to study how contrast enhancement and spatial filtering affect image intensity, noise, and visual quality before later stages such as segmentation or feature extraction.

## Project Workflow

### 1. Image Generation
A synthetic peripheral blood smear is created using Python and OpenCV. The image contains red blood cells and white blood cells, with mild contrast reduction and added Gaussian and salt-and-pepper noise to make the preprocessing effects easier to observe.

The generated color image is then converted to grayscale.

<img width="811" height="225" alt="image" src="https://github.com/user-attachments/assets/aec722d4-68db-4c9a-b988-e847b1faaae6" />


### 2. Histogram and CDF
The grayscale image histogram is calculated to show the distribution of pixel intensities.

The cumulative distribution function (CDF) is also calculated using the cumulative sum of the histogram. This shows how many pixels have intensity values less than or equal to each gray level.

<img width="753" height="200" alt="image" src="https://github.com/user-attachments/assets/3bfa7680-12b5-49f9-83b3-5f299b155784" />


### 3. Global Histogram Equalization
Global histogram equalization is applied using OpenCV's `cv2.equalizeHist()`.

This redistributes the intensity values across a wider range and improves the overall contrast of the image.

<img width="425" height="283" alt="image" src="https://github.com/user-attachments/assets/32a6ecc2-e89c-4dee-941f-5467b830fa6d" />


### 4. Manual Histogram Equalization
Histogram equalization is also implemented manually using the histogram and CDF.

A lookup table is created from the CDF equation and applied to the image. The manual result is compared with the OpenCV result to verify the implementation.

<img width="371" height="155" alt="image" src="https://github.com/user-attachments/assets/51353581-b07b-4989-8725-b48a6e051b94" />


### 5. CLAHE
Contrast Limited Adaptive Histogram Equalization (CLAHE) is tested using different clip limits and tile sizes.

Unlike global histogram equalization, CLAHE processes smaller regions of the image separately, making it useful for improving local contrast while limiting excessive enhancement.

<img width="354" height="442" alt="image" src="https://github.com/user-attachments/assets/fd8bc1c2-e4db-483c-8b41-03d91c7e15df" />


### 6. Spatial Filtering
Three spatial filters are applied:

- **Mean Filter:** smooths the image by averaging neighboring pixels.
- **Gaussian Filter:** reduces Gaussian-like noise using weighted averaging.
- **Median Filter:** replaces each pixel with the median value of its neighborhood and is especially useful for salt-and-pepper noise.
- 
<img width="494" height="295" alt="image" src="https://github.com/user-attachments/assets/56ca36a8-d056-4ce6-8dcc-661b3217d7a8" />

### 7. Quantitative Comparison
The preprocessing results are compared using:

- Minimum intensity
- Maximum intensity
- Mean intensity
- Standard deviation
- Histograms

This helps show how each preprocessing method changes the image intensity distribution.

### 8. Preprocessing Selection
The results show that different preprocessing methods are useful for different image problems:

- Global histogram equalization for poor overall contrast
- CLAHE for non-uniform local contrast
- Median filtering for salt-and-pepper noise
- Gaussian filtering for Gaussian-like noise

### 9. Data Leakage
The project also considers data leakage in machine-learning pipelines.

Preprocessing settings should be selected using the training data only and then applied unchanged to the test data. Using test data while selecting preprocessing settings can lead to misleading evaluation results.

### 10. Preprocessing Pipeline Comparison
Two preprocessing pipelines are compared:

- Median filtering followed by global histogram equalization
- CLAHE followed by median filtering

The outputs are compared visually and using Mean Absolute Difference (MAD), showing that changing the order of preprocessing operations can produce different results.

## Technologies Used

- Python
- NumPy
- OpenCV
- Matplotlib
- Jupyter Notebook
