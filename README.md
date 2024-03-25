# PyTorch implementation of UNet++ (Nested U-Net)
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

This repository contains code for a image segmentation model based on [UNet++: A Nested U-Net Architecture for Medical Image Segmentation](https://arxiv.org/abs/1807.10165) implemented in PyTorch.

[**NEW**] Add support for multi-class segmentation dataset.

[**NEW**] Add support for PyTorch 1.x.


## Requirements
- PyTorch 1.x or 0.41

## Installation
1. Create an anaconda environment.
```sh
conda create -n=<env_name> python=3.6 anaconda
conda activate <env_name>
```
2. Install PyTorch.
```sh
conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
```
3. Install pip packages.
```sh
pip install -r requirements.txt
```

## Training on ica dataset
Make sure to put the files as the following structure (e.g. the number of classes is 2):
```
inputs
└── <ica>
    ├── images
    |   ├── nj_100_1_LCA_RAO.png
    │   ├── nj_100_2_LCA_RAO.png
    │   ├── nj_100_1_LCA_RAO.png
    │   ├── ...
    |
    └── masks/0
        ├── nj_100_1_LCA_RAO.png
        ├── nj_100_2_LCA_RAO.png
        ├── nj_100_1_LCA_RAO.png
        ├── ...
```

1. Train the model.
```
python train.py --dataset <dataset name> --arch NestedUNet --img_ext .jpg --mask_ext .png
```
2. Evaluate.
```
python val.py --name <dataset name>_NestedUNet_woDS
```

## Results
### ica (96x96)

Here is the results on ica dataset (96x96) .

| Model                           |   IoU   |  Loss   |
|:------------------------------- |:-------:|:-------:|
| U-Net                           |  0.839  |  0.365  |
| Nested U-Net                    |  0.842  |**0.354**|
| Nested U-Net w/ Deepsupervision |**0.843**|  0.362  |
