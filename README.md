# A Fully Automatic Method to Segment Choroid Plexuses using Conventional MRI Sequences

Choroid plexus (CP) is a structure of the brain ventricular system that demonstrated an involvement in the inflammatory process of patients with neurological diseases like multiple sclerosis. However, its role in the pathophysiology of these diseases needs to be further explored but its manual delineation on MRI is time-consuming. We developed a fully-automatic method to segment CP using 3DT1-weighted and FLAIR MRI sequences. The algorithm proved to be accurate, easy to implement and do not require an initial training phase on huge amount of data, being generalizable and a fast tool to potentially be included in a clinical setting.

CITATION

Our paper describing an automatic method to segment choroid plexus in multiple sclerosis patients using 3D T1-weighted and FLAIR brain MRI has been published on the Journal of Magnetic Resonance Imaging. If you use this algorithm, please cite our paper: 

Storelli, L., Pagani, E., Rubin, M., Margoni, M., Filippi, M., Rocca, MA., 2023. A Fully Automatic Method to Segment Choroid Plexuses in Multiple Sclerosis Using Conventional MRI Sequences. Journal of Magnetic Resonance Imaging.

PIPELINE

![image](https://github.com/lorestore/NRU-CP_segmentation/assets/64906745/6a9b41f5-8bdf-4032-88ca-048ef95edb44)


Examples of choroid plexus segmentations from three automatic pipelines: FreeSurfer (FS), the recently published FS extension (FS-GMM) and the proposed method (FLAIR+T1 GMM) 

![image](https://github.com/lorestore/NRU-CP_segmentation/assets/64906745/f2eafe76-f1bd-4b84-99e6-f7feba059a7c)

REQUIRED PACKAGES

•	FSL - for brain tissue segmentation and image registration

•	MATLAB (version 2017 or later) with SPM - for CP segmentation

HOW TO RUN THE PIPELINE

The current version of the script requires FSL-SIENAX processed files for WM, GM, CSF binary segmentation masks, and white matter lesions (if present) already segmented on FLAIR;

Before running CP segmentation, some initial image registrations are needed. Having installed FSL tool, run in the terminal:

  1.	Image registration of the ventricle mask in the standard space into the T1 space

    flirt -in <ventricle_mask_in_standard_space> -ref <T1_image> -applyxfm -init <standard_space_to_T1.mat> -out <ventricle_on_T1>

    fslmaths <ventricle_on_T1> -thr 0.99 -bin ventricle_ss_bin.nii.gz

  2.	Image registration of T1 image to the FLAIR space

    flirt -in <T1_image> -ref <FLAIR_image> -omat T1_to_flair.mat 

Please be sure that all the required files are in the same folder and are named as: ‘wm.nii’ (white matter binary mask), ‘gm.nii’ (gray matter binary mask), ‘csf.nii’ (cerebrospinal fluids binary mask), ‘flair.nii’, ‘FLAIR_LesMask.nii’ (white matter lesions binary mask, if present)

Please be sure that both codes CP_GMM_segm.p and Divide_CSF.p are in the same folder

Then in the terminal, run:

  matlab -nodesktop -nosplash -r "addpath <path_to_the_program>; addpath <path_to_spm>; CP_GMM_segm; quit;"

The resulting choroid plexus segmentation mask is named: ‘CP_mask.nii’

Contacts

rocca.mara@hsr.it

storelli.loredana@hsr.it

