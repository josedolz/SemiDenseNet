# SemiDenseNet
This repository contains the code of the network that we employed in the iSEG Grand MICCAI Challenge 2017, infant brain segmentation. This network extends out previous work in 3D fully convolutional neural network that was employed in our work: [3D fully convolutional networks for subcortical segmentation in MRI: A large-scale study](http://www.sciencedirect.com/science/article/pii/S1053811917303324), which can be found here : (https://github.com/josedolz/LiviaNET/).

<br>
<img src="https://github.com/josedolz/SemiDenseNet/blob/master/Images/brainModalities.png" />
<br>

IMPORTANT: This Net is not the one that best performed in the iSEG Challenge, but the one with an individual path per modality and a late fusion stage to merge learned features (See figure). In case you want to adapt this net to the best performing net, you should remove one of the paths and merge T1 and T2 modalities at the input of the network. 

<br>
<img src="https://github.com/josedolz/SemiDenseNet/blob/master/Images/SemiDenseNET.png" />
<br>

NOTE: The submission of this work is under review. If you use this code for your research, please consider citing the papers:

- Dolz J, Desrosiers C, Ben Ayed I. "[3D fully convolutional networks for subcortical segmentation in MRI: A large-scale study."](http://www.sciencedirect.com/science/article/pii/S1053811917303324) NeuroImage (2017).

- Dolz J, Desrosiers C, Wang L, Yuang J, Shen D, Ben Ayed I. "[Deep CNN ensembles and suggestive annotations for infant brain MRI segmentation"](https://arxiv.org/pdf/1712.05319.pdf)

The main differences with respect to that network are:
- The use of multi-modal images (MR-T1 and T2) processed in independent paths.
- Feature maps from all the layers are connected to the first fully connected layer (That is why we call it: Semi-dense Net).

## Requirements

- The code has been written in Python (2.7) and requires [Theano](http://deeplearning.net/software/theano/)
- You should also have installed [scipy](https://www.scipy.org/)
- (Optional) The code allows to load images in Matlab and Nifti formats. If you wish to use nifti formats you should install [nibabel](http://nipy.org/nibabel/) 
- Since, as you might now, sharing medical data is not a good-practice, I did not include any sample in the corresponding folders. To make your experiments you must include your data in the repositories indicated in the config file (LiviaNET_Config.ini and LiviaNET_Segmentation.ini)

## Running the code

Running the code actually works in the same way that LiviaNet. Just a reminder if you do not want to check the documentation from that net :)

## Training

### How do I train my own architecture from scratch?

To start with your own architecture, you have to modify the file "LiviaNET_Config.ini" according to your requirements.

Then you simply have to write in the command line:

```
python ./networkTraining.py ./LiviaNET_Config.ini 0
```

This will save, after each epoch, the updated trained model.

If you use GPU, after nearly 5 minutes you will have your trained model from the example.

### Can I re-start the training from another epoch?

Imagine that after two days of training your model, and just before you have your new model ready to be evaluated, your computer breaks down. Do not panic!!! You will have only to re-start the training from the last epoch in which the model was saved (Let's say epoch 20) as follows:

```
python ./networkTraining.py ./LiviaNET_Config.ini 1 ./outputFiles/LiviaNet_Test/Networks/liviaTest_Epoch20
```

### Ok, cool. And what about employing pre-trained models?

Yes, you can also do that. Instead of loading a whole model, which limits somehow the usability of loading pre-trained models, this code allows to load weights for each layer independently. Therefore, weights for each layer have to be saved in an independent file. In its current version (v1.0) weights files must be in numpy format (.npy).

For that you will have to specify in the "LiviaNET_Config.ini" file the folder where the weights are saved ("weights folderName") and in which layers you want to use transfer learning ("weights trained indexes").

## Testing

### How can I use a trained model?

Once you are satisfied with your training, you can evaluate it by writing this in the command line:

```
python ./networkSegmentation.py ./LiviaNET_Segmentation.ini ./outputFiles/LiviaNet_Test/Networks/liviaTest_EpochX
```
where X denotes the last (or desired) epoch in which the model was saved.

### Versions
- Version 1.0. 
  * October,20th. 2017
    * Network processes multi-modal data (so far only two-modalities) and fuses the learned features before the first fully convolution connected layer.


### Known problems
* In some computers I tried, when running in CPU, it complains about the type of some tensors. The work-around I have found is just to set some theano flags at the beginning of the scripts. Something like:

```
THEANO_FLAGS='floatX=float32' python ./networkTraining.py ./LiviaNET_Config.ini 0
```

You can contact me at: jose.dolz.upv@gmail.com
