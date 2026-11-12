# Adaptive Document Restoration Using Degradation Analysis and Classical Image Processing Techniques

## Project Description

A MATLAB-based Digital Image Processing project that restores degraded scans of historical handwritten manuscripts using classical image-processing techniques.

The system addresses common document degradations such as:
- Uneven illumination
- Faded handwriting
- Background stains
- Reverse-side ink bleed-through (show-through)
- Book-edge shadows
- Folds, creases and smears

The objective is to improve document readability while preserving the natural thickness and structure of handwritten strokes.

## Summary

The proposed system uses an adaptive, structure-based image-restoration pipeline instead of relying mainly on global histogram enhancement.

The pipeline analyses each manuscript page, estimates the paper background, detects handwriting using morphological operations and noise-adaptive thresholds, removes unwanted regions and reconstructs the page with a soft alpha matte.

Two major adaptive mechanisms are incorporated:

1. **Page Classification:** Each page is classified as faint, normal, bold or noisy, and suitable processing parameters are selected.
2. **Self-Check Restoration Loop:** The restored image is evaluated for thickened strokes, lost ink, unwanted components and pale handwriting. Parameters are adjusted and restoration is repeated, up to three attempts, retaining the best result.

The system uses classical image processing without deep learning or language models.

## Course Concepts Used

### Unit 1: Digital Image Fundamentals

1. Image sampling and resizing using bicubic interpolation.
2. Quantisation using 8-bit grayscale representation (256 intensity levels).
3. Pixel relationships and 8-connectivity.
4. Connected-component analysis.
5. Linear and nonlinear image operations.

### Unit 2: Image Transforms

1. Gaussian low-pass filtering and its relationship with frequency-domain filtering.
2. Convolution theorem: Gaussian smoothing in the spatial domain corresponds to Gaussian low-pass filtering in the DFT domain.
3. High-frequency residual estimation.
4. Median Absolute Deviation (MAD) for robust noise estimation.

**Note:** The final pipeline does not contain an explicit DFT or Haar transform operation. These were explored earlier but did not provide additional benefits on the tested pages.

### Unit 3: Image Enhancement, Filtering and Restoration

1. Gamma or power-law transformation in the alpha matte.
2. Histogram equalisation, CLAHE and histogram matching as comparison methods.
3. Gaussian and median filtering.
4. Arithmetic operations such as division and subtraction.
5. Background estimation and illumination correction.
6. Noise-adaptive thresholding and restoration.

### Unit 4: Morphological and Colour Image Processing

1. Morphological closing and opening.
2. Black top-hat transformation.
3. Morphological reconstruction and hysteresis.
4. Hole filling and area opening.
5. Dilation and connected-component processing.
6. Lab colour model for identifying coloured mounts and stains.

## Additional Concepts Used

1. Otsu thresholding for dark scanner-border detection.
2. Adaptive page-class selection using ink contrast, roughness and background variation.
3. Self-check restoration loop with parameter correction.
4. Mirrored-slant show-through detection using Sobel gradient orientation.
5. Shape-based detection of ring stains, book edges, creases and slivers.
6. Component filtering to remove weak unsupported regions.
7. Soft alpha matte with gamma correction.
8. Selective and capped darkening of confirmed handwriting.
9. Foreground and background separation using region filling.
10. Quantitative evaluation using PSNR, SSIM, Fisher ratio, entropy and separation measures.

## Dataset

The project was evaluated using:

- Ten real degraded handwritten historical manuscript pages.
- Six clean pages used for synthetic degradation experiments.

The synthetic degradation included:
- Artificial stains
- Uneven illumination
- Mirrored show-through
- Image noise

The real manuscript pages were used for qualitative restoration evaluation. The synthetic images were used for quantitative evaluation because clean reference images were available for that experiment.

Place the input manuscript images inside the `data/` directory.

Add the dataset source and usage information here if the images are obtained from an external dataset.

## Novelty

The contribution of this project lies in combining classical image-processing techniques with page-level adaptation.

1. **Adaptive Page Classification:** Selects processing profiles according to the degradation characteristics of each page.
2. **Self-Check Restoration Loop:** Evaluates the restoration, identifies specific errors and adjusts the corresponding parameters automatically.
3. **Mirrored-Slant Show-Through Detection:** Uses handwriting orientation to distinguish reverse-side writing from faint real handwriting.
4. **Soft Alpha Matte:** Preserves natural handwriting thickness without relying on a single hard global threshold.
5. **Selective Darkening:** Enhances confirmed handwriting while avoiding unnecessary darkening of the background.
6. **Foreground and Background Separation:** Exports accepted handwriting and the reconstructed background as separate images.

These contributions represent the combination and adaptation developed within this course project; no individual technique is claimed to be new to the research field.

## Contributors

- [Contributor 1 – Name and SRN]
- [Contributor 2 – Name and SRN]

## Steps to Run

1. Install MATLAB.
2. Clone or download this repository.
3. Open the project directory in MATLAB.
4. Place the input manuscript images inside the `data/` folder.
5. Run the project's main MATLAB restoration script.
6. Inspect the restored images, intermediate processing stages and evaluation results inside the `outputs/` folder.

**Note:** Replace this instruction with the exact MATLAB entry-point filename once the source code is added.

## Outputs

The system generates the following outputs:

- Restored grayscale manuscript images.
- Restored colour manuscript images.
- Foreground handwriting with a transparent background.
- Foreground image on a white background.
- Binary foreground mask.
- Red debug overlay showing accepted handwriting pixels.
- Background-only image with handwriting regions filled using surrounding information.
- Quantitative evaluation tables and metrics.

## Results

### Synthetic Degradation Evaluation

| Method | PSNR (dB) | SSIM | Text F1 |
|---|---:|---:|---:|
| Degraded Input | 11.81 | 0.804 | 0.955 |
| Histogram Equalisation | 5.96 | 0.267 | 0.237 |
| CLAHE | 11.19 | 0.353 | 0.670 |
| Paper-style AHM + Median (Approx.) | 13.62 | 0.840 | 0.623 |
| Proposed Method | 26.39 | 0.960 | 0.930 |

### Qualitative Results

- Ten real manuscript pages were processed.
- Reverse-side show-through was reduced on page 4.
- Book-edge shadows were removed from page 5 while retaining most faint handwriting.
- Adaptive processing improved the readability of faint and stained pages.
- Foreground and background components were exported separately.

### Evaluation Note

The clean reference used in the synthetic experiment was generated from an earlier output of the system. Therefore, the reported PSNR and SSIM values may favour the proposed method and should not be interpreted as an independent benchmark.

Real manuscript pages did not have clean ground-truth references. Additional measures were used to evaluate background flatness and ink separation.

## References

1. F. Suleiman et al., "Adaptive Enhancement for Scanned Historical Document Images," 2021 IEEE 4th International Conference on Electronics and Communication Engineering (ICECE), 2021. DOI: 10.1109/ICECE54449.2021.9674392.
2. Digital Image Processing course materials, PES University.

## Limitations and Future Work

1. A few faint mirrored fragments and specks remain on page 4.
2. The end of a faint handwriting line and part of the page number are lost on page 5.
3. A dark smudge remains on page 6.
4. A thin crease may remain on page 9.
5. Small dots remain near the edge of page 10.
6. The mirrored-slant test may miss show-through when the handwriting is nearly upright.
7. Real manuscript pages do not have clean ground-truth images for direct quality evaluation.

### Future Work

- Evaluate the system using DIBCO datasets with ground-truth images.
- Improve detection of mirrored writing overlapping genuine handwriting.
- Improve preservation of extremely faint handwriting.
- Explore explicit transform-domain noise estimation.
- Extend testing to a larger collection of degraded historical documents.
