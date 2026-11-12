# Adaptive Document Restoration Using Degradation Analysis and Classical Image Processing Techniques

## Project Description

A MATLAB-based Digital Image Processing project that restores degraded scans of handwritten historical manuscripts using classical image-processing techniques.

The system addresses uneven illumination, faded ink, background stains, reverse-side ink show-through, folds and book-edge shadows.

## Summary

The project aims to improve the readability of historical handwritten documents while preserving the natural thickness of handwriting strokes.

The proposed pipeline analyses each page, estimates background illumination, detects ink using morphological operations and noise-adaptive thresholds, removes unwanted regions and generates restored grayscale and colour images.

It uses adaptive page classification and a self-check restoration loop to adjust processing parameters according to the degradation characteristics of each page.

The implementation uses classical image processing without deep learning or language models.

## Course Concepts Used

### Unit 1: Pixel Relationships and Sampling
1. Image resizing using bicubic interpolation.
2. 8-bit grayscale quantisation.
3. 8-connectivity and connected component analysis.

### Unit 2: Image Transforms
1. Gaussian low-pass filtering.
2. DFT-domain interpretation of Gaussian smoothing.
3. High-frequency residual and Median Absolute Deviation (MAD) for noise estimation.

Note: The final pipeline does not contain an explicit DFT or Haar transform operation.

### Unit 3: Histogram Processing and Restoration
1. Otsu thresholding for border detection.
2. Histogram equalisation and CLAHE as comparison methods.
3. Gaussian and median filtering.
4. Background estimation and illumination correction.

### Unit 4: Morphological and Colour Processing
1. Morphological closing.
2. Black top-hat transformation.
3. Morphological reconstruction and hysteresis.
4. Area opening and dilation.
5. Lab colour model.

## Additional Concepts Used

1. Adaptive page classification (faint, normal, bold and noisy).
2. Self-check restoration loop.
3. Mirrored-slant show-through detection using Sobel gradient orientation.
4. Soft alpha matte with gamma correction.
5. Selective darkening of confirmed ink.
6. Foreground and background separation.
7. Connected-component shape analysis.

## Dataset

The project was evaluated using:

- Ten real degraded historical manuscript pages.
- Six clean pages used for synthetic degradation testing.

The synthetic degradation included stains, uneven illumination, mirrored show-through and noise.

Input images must be placed in the `data/` folder.

## Novelty

The project contribution is the combination of adaptive and structure-based restoration techniques.

1. Page-level classification selects suitable processing parameters.
2. A self-check loop identifies restoration errors and adjusts parameters.
3. A mirrored-slant test helps distinguish reverse-side show-through from faint real handwriting.
4. A soft alpha matte preserves natural handwriting thickness.
5. Foreground and background images are exported separately.

No individual technique is claimed to be new to the research field.

## Contributors

1. Nagaraju D V
2. V Sai Ankit Jadav

## Steps to Run

1. Install MATLAB.
2. Clone or download the repository.
3. Open the project folder in MATLAB.
4. Place the input manuscript images inside `data/`.
5. Run the original MATLAB entry-point script included in the repository.
6. Check the restored images and intermediate results inside `outputs/`.

Note: Update this section with the exact MATLAB script filename and execution command when the source files are uploaded.

## Outputs

The project generates:

- Restored grayscale images.
- Restored colour images.
- Foreground handwriting with transparent background.
- Foreground image on white background.
- Binary foreground mask.
- Debug overlay.
- Background-only image.
- Quantitative evaluation results.

## Results

Synthetic degradation evaluation:

| Method | PSNR (dB) | SSIM | Text F1 |
|---|---:|---:|---:|
| Degraded Input | 11.81 | 0.804 | 0.955 |
| Histogram Equalisation | 5.96 | 0.267 | 0.237 |
| CLAHE | 11.19 | 0.353 | 0.670 |
| Paper-style AHM + Median | 13.62 | 0.840 | 0.623 |
| Proposed Method | 26.39 | 0.960 | 0.930 |

Evaluation note: The clean reference used in the synthetic test was generated from an earlier output of the system. Therefore, the results may favour the proposed method and should not be interpreted as an independent ground-truth benchmark.

## References

1. F. Suleiman et al., "Adaptive Enhancement for Scanned Historical Document Images," IEEE ICECE, 2021. DOI: 10.1109/ICECE54449.2021.9674392.
2. Digital Image Processing course materials, PES University.

## Limitations and Future Work

1. Some faint handwriting fragments and small stains remain in a few restored pages.
2. The mirrored-slant test may miss show-through when handwriting is nearly upright.
3. Some faint real strokes can be lost during restoration.
4. Real manuscript pages do not have clean ground-truth images for direct PSNR and SSIM evaluation.
5. Future work includes evaluation using DIBCO datasets with ground truth and improving overlapping show-through detection.
