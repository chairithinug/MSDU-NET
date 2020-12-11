# MSDU-NET
This is my implementation of MSDU-Net based on the paper [MSDU-net: A Multi-Scale Dilated U-net for
Blur Detection] (https://arxiv.org/pdf/2006.03182.pdf) by Fan Yang and Xiao Xiao. Please visit the paper for more detail.
There might be mistakes in the implementation. I do not guarantee the exact accuracy/performance as claimed in the paper. I just want to share my understanding and model after reading this paper.

# Model
It consists of 4 extractors, which uses dilated convolutions, in front of the UNet. Each extractor gets the same input image but feeds its output to the different level of the UNet. Please look at the images inside the paper for greater detail.
![Model's architecture](/images/msdu-net.png)

## Dataset
I trained the model from a combined dataset between CUHK and DUT for blur detection. 
CUHK contains both motion-blurred images and defocused images. I splitted the data into training and test sets (800 training, 200 test) in the way that preserved the ratio between two kinds of blur.
DUT contains both training and test sets (600 training, 500 test) as the data has been splitted by the authors.

The new dataset consists of 1400 pairs of images and ground truth images as a training set and 700 pairs as a test set.

## Hyperparameters
My input images are of 128x128 RGB images with 128x128 1-channel grayscale ground truth masks.
The learning rate is 0.01, momentum is 0.9, weight_decay is 5e-4, batch_size is 16, epochs is 100 as described in the paper. I have not explored different sets of hyperparameters yet.

## Performance
The results I got seems decent enough but I have not compared the proposed architecture to different architectures yet.

## My machine
The model was trained using Nvidia RTX 3070 with 8 GB of memory.