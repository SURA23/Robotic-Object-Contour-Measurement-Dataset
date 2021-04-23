# Robotic-Object-Contour-Measurement-Dataset
A dataset for one-shot learning based contour of intereset extraction

This folder contains the ROCM dataset and the MF-ODS evaluation scripts.

1. ROCM Dataset

The robotic object contour measurement (ROCM) datatset is built for evaluating the performance of ONE-SHOT learning based contour primitive of interest (CPI) extraction, as presented in the ICRA 2021 paper [1].


2. MF-ODS evaluation scripts:
Since CPI map is a special case of edge/contour map, we follow the edge/contour/boundary detection works[2] and use the MF-ODS score to evaluate the model performance.



3. The dataset folder is arranged as follows:

|--- readme.txt

|--- test-pairs

      |--- query-images (used for testing)
            |--- object_*_*.jpg
      |--- query-labels (used as CPI groundtruths)
            |--- object_*_*_line/arc_*.png

      |--- support-images (used for support branch, 1st-frame mode)
            |--- object_*_1.jpg
      |--- support-labels (CPI annotation)
            |--- object_*_1_line/arc_*.png
      |--- support-masks (object foreground annotation)
            |--- object_*_1.png

      |--- support-labels-extra (used for support branch, cross-device mode)
            |--- object_*_1.jpg
      |--- support-images-extra (CPI annotation)
            |--- object_*_1_line/arc_*.png
      |--- support-masks-extra (object foreground annotation)
            |--- object_*_1.png

Example:

To test on the circular CPI on object 1 in the query image /query-images/object_1_5.jpg, 
we use /query-labels/object_1_5_arc_0.png as the CPI GT,

then,
use /query-images/object_1_5.jpg as the query input, 
use /support-images/object_1_1.jpg as the support image, 
use /support-labels/object_1_1_arc_0.png as the support CPI annotation,
use /support-masks/object_1_1.png as the support object foreground annotation,
to predict the CPI image /test-rsts/object_1_5_arc_0.png using one-shot learning based CNN model.

To evaluate the accuracy of CPI extraction, we compare  /query-labels/object_1_5_arc_0.png and /test-rsts/object_1_5_arc_0.png using the MF-ODS evaluation scripts.

Note that the folders with the suffix '-extra' and the folders without the suffix '-extra' only differ in how the support image is captured, which correspond to the '1st frame mode' and 'cross-device mode'. More details is found in [1].

4. The MF-ODS evaluation scripts are provided in
|--- eval
|--- eval-extras

Configure the paths in demoBatchEval.m and run it with Matlab.
Note that this code is based on [2], and the misalignment tolerance parameter is set in correspondPixels.cc. If you need modify it, you need to re-compile correspondPixels.cc to correspondPixels.mexa64 using build.sh.


[1] Contour Primitive of Interest Extraction Network Based on One-Shot Learning for Object-Agnostic Vision Measurement, ICRA 2021, https://arxiv.org/abs/2010.03325
[2] https://github.com/Lavender105/DFF
