# Dense Extreme Inception Network: Towards a Robust CNN Model for Edge Detection (DexiNed)

<!-- ```diff
- Sorry for any inconvenience, we are updating the repo
``` -->

This work presents a new Convolutional Neural Network (CNN) arquitecture for edge detection. Unlike of the state-of-the-art CNN based edge detectors, this models has a single training stage, but it is still able to overcome those models in the edge detection datasets. Moreover, Dexined does not need pre-trained weights, and it is trained from the scratch with fewer parameters tunning.

<div style="text-align:center"><img src='figs/DexiNed_banner.png' width=800>

# Table of Contents

* [Geting Started](#geting-started)
* [Datasets](#datasets)
* [Performance](#performance)
* [Citation](#citation)
* [Aknowledgement](#aknowledgement)

# Geting Started

 Before starting to use this model,  there are some requerements to fullfile.
 
## Requirements

* [TensorFlow>=1.8 <=1.13.1](https://www.tensorflow.org) (tested on such versions)
* [OpenCV](https://pypi.org/project/opencv-python/)
* [Matplotlib](https://matplotlib.org/3.1.1/users/installing.html)
* Other package like Numpy, h5py, PIL. 

Once the packages are installed,  clone this repo as follow: 

    git clone https://github.com/xavysp/DexiNed.git
    cd DexiNed

## Project Architecture

```
├── data                        # sample images for testing
|   ├── lena_std.tif            # sample 1
|   └── stonehengeuk.jpg        # sample 2
├── figs                        # Images used in README.md
|   └── DexiNed_banner.png      # DexiNed banner
├── models                      # tensorflow model file  
|   └── dexined.py              # DexiNed class
├── utls                        # a series of tools used in this repo
|   └── dataset_manager.py      # tools for dataset managing
|   └── losses.py               # Loss function used to train DexiNed 
|   └── utls.py                 # miscellaneous tool functions
├── run_model.py                # the main python file with main functions and parameter settings
└── test.py                     # the script to run the test experiment
└── train.py                    # the script to run the train experiment
```

As described above, run_model.py has the parameters settings, wether DexiNed is used for training or testing, before thoses processes the parameters need to be set. As highlighted, DexiNed is trained just one time with our proposed dataset BIPED so in "--train_dataset" as the default setting is BIDEP; however, in the testing stage (--test_dataset), any dataset can be used, even CLASSIC, which are any arvitrare image downloaded from internet but to evaluate with single images or CLASSIC "--use_dataset" have to be in FALSE mode. Whenever a dataset is used to test or train DexiNed the arguments have to heve the list of training or testingn files files (--train_list, --test_list). Pay attention in the parameters settings, and change whatever you want, like ''--image_width'' or ''--image_height''. To test lena image I have set 512x512.
```
parser.add_argument('--train_dataset', default='BIPED', choices=['BIPED','BSDS'])
parser.add_argument('--test_dataset', default='CLASSIC', choices=['BIPED', 'BSDS','MULTICUE','NYUD','PASCAL','CID'])
parser.add_argument('--dataset_dir',default=None,type=str)
parser.add_argument('--dataset_augmented', default=True,type=bool)
parser.add_argument('--train_list',default='train_rgb.lst', type=str)
parser.add_argument('--test_list', default='test_pair.lst',type=str)  
```

## Test
Before test the DexiNed model it is necesarry to download the checkpoint here [Checkpoint from Drive](https://drive.google.com/open?id=1fLBpOrSXC2VOWUvDtNGyrHcuB2IB-4_D) and save this files intro the DexiNed folder like: DexiNed/checkpoints/(here) then run as follow:

    python run_model.py 
Make sure that in run_model.py the test setting be as:
```parser.add_argument('--model_state', default='test', choices=['train','test','None'])```

## Train

    python run_model.py 
Make sure that in run_model.py the test setting be as:
```parser.add_argument('--model_state', default='train', choices=['train','test','None'])```

# Datasets

## Trained dataset

BIPED (Barcelona Images for Perceptual Edge Detection): This dataset is collected and annotated in the edge level for this work. See more details and download [here](https://xavysp.github.io/MBIPED/)

## Tested datasets

Edge detection dataset
* [BIPED](https://xavysp.github.io/MBIPED/) and [MDBD](http://serre-lab.clps.brown.edu/resource/multicue/)

Non-edge detection datasets

* [CID](http://www.cs.rug.nl/~imaging/databases/contour_database/contour_database.html) <!-- * [DCD](http://www.cs.cmu.edu/~mengtial/proj/sketch/)-->, [BSDS300](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/bsds/), [BSDS500](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/bsds/), [NYUD](https://cs.nyu.edu/~silberman/datasets/nyu_depth_v2.html), and [PASCAL-context](https://cs.stanford.edu/~roozbeh/pascal-context/)

# Performance
<center>

|     Methods    |    ODS   |    ODS   |    AP    |
| -------------- | ---------| -------- | -------- |
| `[SED]()`      | `60.2` | `74.3` | `43.6` |
| `[HED]()`      | `60.8` | `74.3` | `44.3` |
| `[RCF]()`      | `60.8` | `74.3` | `44.3` |
| `[BDCN]()`     | `60.8` | `74.3` | `44.3` |
| `DexiNed(Ours)`| `60.8` | `74.3` | `44.3` |
</center>

# Citation
Please cite our paper if you find helpful,
```
@InProceedings{soria2020dexined,
    title={Dense Extreme Inception Network: Towards a Robust CNN Model for Edge Detection},
    author={Xavier Soria and Edgar Riba and Angel Sappa},
    booktitle={The IEEE Winter Conference on Applications of Computer Vision (WACV '20)},
    year={2020}
}
```

<!--```
@misc{soria2020dexined_ext,
    title={Towards a Robust Deep Learning Model for Edge Detection},
    author={Xavier Soria and Edgar Riba and Angel Sappa},
    year={2020},
    eprint={000000000},
    archivePrefix={arXiv},
    primaryClass={cs.CV}
```-->
# Acnowledgement
