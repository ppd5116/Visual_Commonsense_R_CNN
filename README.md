# Utility functions

This folder contain utility functions that are not used in the
core library, but are useful for building models or training
code using the config system.

1. VC Feature
   - **Effective**: The visual common sense region-based convolutional neural network framework encodes the``sense-making'' knowledge between object Region of Interests (RoIs) by utilizing Vc R-CNN unique causal intervention feature rather than the conventional likelihood that has been used in previous techniques, namely, Faster R-CNN. 
   - **Easy to Use**: As hightighted in the Vc R-CNNpaper, the Visual Commonsense Feature is extracted by providing the coordinates of Region of Interests bounded boxes. Following this, the VC Feature can **just concatenated** on the previous visual object features (e.g., Up-Down Feature) and it is then prepared to proceed further in the network feature learning method.  
   - **Easy to Expand**: With a learned VC R-CNN framework, it is simpler to extract the Visual Common features for any set of image datasets and prepare them as an ``augmentation feature'' for the currently used representation conveniently.
2. VC R-CNN
   - **Support customized dataset**: Users and/or Readers can easily append MS-COCO based datasets to train VC R-CNN on other set of image classes.

### How to use after download

- Unzip the file with command:
```bash
tar -xzvf file_name
```

- The feature format (The shape of each numpy file is [n x 1024]):
```
coco_trainval/test_year
 |---image_id1.npy
 |---image_id2.npy
  ...
 |---image_idN.npy
```

- Concatenate on the previous feature in the downstream task training.

## VC R-CNN Framework

### Installation
Please check [INSTALL.md](INSTALL.md) for installation instructions.

** Extracting features of customized dataset**

On using the trained VC R-CNN, it is possible to directly extract the Visual Commonsense Features, with the provided raw images and bounding box coordinates. 
Please refer to `openimages.py` and `vcr.py`. 

### Perform Training on COCO Dataset

#### Prepare Training Data

1. First, you need to download the COCO dataset and annotations. Assumption: save file in the path:  `/path_to_COCO_dataset/`
2. Second, updating the path present in this path: `vc_rcnn/config/paths_catalog.py`, comprising of the folders `DATA_DIR` and `DATASETS path`.

#### Training Parameters

- `default.py`: `OUTPUT_DIR` => denotes the model output dir. 
- `TENSORBOARD_EXPERIMENT` => denotes tensorboard loger output dir. 
- `SOLVER.IMS_PER_BATCH` => denotes the total number of images per batch.
- Config file (e.g., `e2e_mask_rcnn_R_101_FPN_1x.yaml`): Main parameters that are required for the efficient functioning => training schedule, learning rate, and the utilized dataset. 
- Visual Commonsense Parameters: present at the end of `default.py` with annotations. Users can make changes according to their own situation.

According to the authors of the paper, the operation of concatenation is overly simple and and may not produce the Visual Commonsense R-CNN model's output to its maximum efficiency. As the author suggested, I tried on working expaning the bandwidth, however I wasn't able to come up with accurate results. This ReadMe file has been based on the author's paper code ReadMe file as the building of this entire network has been based of the paper's given code. 
