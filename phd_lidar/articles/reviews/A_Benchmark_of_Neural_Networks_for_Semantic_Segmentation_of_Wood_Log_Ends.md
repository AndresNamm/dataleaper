
# Review: A Benchmark of Neural Networks for Semantic Segmentation of Wood Log Ends

## Metadata
*   **Authors:** Dorian Martinetto, Georg Wimmer, Phuc Ngo, Frédéric Mothe, Alexandre Piboule, Andreas Uhl, Isabelle Debled-Rennesson, Fleur Longuetaud
*   **Journal:** IEEE Access
*   **Year:** 2025
*   **Volume:** 13
*   **Pages:** 180344-180354
*   **DOI:** 10.1109/ACCESS.2025.3622419

## Summary
This paper presents a benchmark of deep learning-based methods for the semantic segmentation of wood log ends (cross-sections) in images. The study focuses on segmenting the central log in an image, ignoring background logs. It introduces a new dataset of 1345 manually segmented oak log end images, supplemented by 855 softwood images (Douglas fir and spruce). Five state-of-the-art architectures were tested: Mask R-CNN, U-Net, PointRend, YOLOv11, and OneFormer.

## Methodology

### Datasets
1.  **Oak Dataset:** 1345 images of oak log ends, manually segmented under-bark. Collected as part of the Biomtrace project.
2.  **Softwood Dataset:** 855 images of Douglas fir and spruce from the TreeTrace project.
3.  **Characteristics:** Varied lighting, weather, camera angles, shadows, paint/dirt/cracks, and obstructions (grass).
4.  **Split:** 5-fold cross-validation on training set (80% train, 20% validation). Independent test set of 250 images (150 oak, 100 softwood).

### Architectures Evaluated
*   **U-Net:** Fully convolutional network, implemented from scratch.
*   **Mask R-CNN:** Instance segmentation model (ResNet-50 backbone), implementation from Detectron2.
*   **PointRend:** Extension of Mask R-CNN for finer segmentation (ResNet-101 backbone), implementation from Detectron2.
*   **YOLOv11:** Real-time object detection/segmentation (YOLOv11x), implementation from Ultralytics.
*   **OneFormer:** Multi-task transformer (Swin backbone), implementation from HuggingFace.

### Evaluation Metrics
*   Precision, Recall, Accuracy, Dice Coefficient, IoU (Intersection over Union), and MCC (Matthews Correlation Coefficient).

## Key Results
*   **PointRend:** Achieved the best overall segmentation quality (highest Dice, IoU, MCC, Accuracy). It produced accurate segmentations with smooth boundaries and no holes.
*   **YOLOv11:** Fastest model (real-time suitable), with highest Recall but lower Precision (tendency to over-segment). Best for applications requiring speed.
*   **OneFormer:** Second best precision, but slowest inference time.
*   **Mask R-CNN:** Reliable results with smooth boundaries, but less precise than PointRend.
*   **U-Net:** Poorest results among the tested architectures, with inaccurate shapes and holes in masks.

| Model | Dice (Test) | IoU (Test) | Inference Time (ms) |
| :--- | :--- | :--- | :--- |
| PointRend | 0.9876 | 0.9758 | 102 |
| YOLOv11 | 0.9856 | 0.9721 | 38 |
| OneFormer | 0.9847 | 0.9702 | 300 |
| Mask R-CNN | 0.9829 | 0.9666 | 79 |
| U-Net | 0.9334 | 0.8822 | 70 |

## Conclusion
For high-precision tasks (e.g., biometric log tracking, quality assessment), **PointRend** is the recommended architecture. For real-time applications where speed is critical, **YOLOv11** is the best choice despite a slight trade-off in segmentation precision. The paper also highlights the importance of the new Oak dataset for training robust models.
