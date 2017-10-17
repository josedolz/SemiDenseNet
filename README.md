# SemiDenseNet
This repository contains the code of the network that we employed in the iSEG Grand MICCAI Challenge 2017, infant brain segmentation. This network extends out previous work in 3D fully convolutional neural network that was employed in our work: [3D fully convolutional networks for subcortical segmentation in MRI: A large-scale study](http://www.sciencedirect.com/science/article/pii/S1053811917303324), which can be found here : (https://github.com/josedolz/LiviaNET/).

NOTE: The submission of this work is under review. If you use this code for your research, please consider citing the papers:

- Dolz J, Desrosiers C, Ben Ayed I. "[3D fully convolutional networks for subcortical segmentation in MRI: A large-scale study."](http://www.sciencedirect.com/science/article/pii/S1053811917303324) NeuroImage (2017).

- Citation coming.

The main differences with respect to that network are:
- The use of multi-modal images (MR-T1 and T2) processed in independent paths.
- Feature maps from all the layers are connected to the first fully connected layer (That is why we call it: Semi-dense Net).

## Requirements

- The code has been written in Python (2.7) and requires [Theano](http://deeplearning.net/software/theano/)
- You should also have installed [scipy](https://www.scipy.org/)
- (Optional) The code allows to load images in Matlab and Nifti formats. If you wish to use nifti formats you should install [nibabel](http://nipy.org/nibabel/) 
