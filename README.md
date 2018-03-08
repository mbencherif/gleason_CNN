## gleason_CNN

This repository contains scripts to reproduce the analysis presented in the paper "Automated Gleason grading of prostate cancer tissue microarrays via deep learning".

The first step is to create image patches for training and validation (``utils/create_patches.py``). We then train a convolutional neural network, e.g. using the MobileNet architecture, to classify image patches as benign, Gleason pattern 3, 4 or 5. Given the small size of our dataset, fine-tuning models pre-trained on ImageNet achieved better results (``gleason_score_finetune.py``).
Once having a good model (the model used in the manuscript is provided: ``model_weights/MobileNet_gleason_weights.h5``), we can use it to produce pixel-level probability maps for entire TMA spots and visualise class-discriminative regions via class activation mappings (``plot_heatmaps_and_CAM.py``). We only want to make predictions on tissue regions, so we automatically create tissue region masks for the TMA images (``utils/create_tissue_masks.py``). We then compare the model's and pathologists' Gleason annotations on the test cohort (``plot_test_cohort_results.ipynb``) and perform survival analysis on the basis of Gleason score assignments (``gleason_survival_analysis.R``).