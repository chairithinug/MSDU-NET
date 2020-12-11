# MSDU-NET
This repo is my implementation of MSDU-Net based on the paper [MSDU-net: A Multi-Scale Dilated U-net for
Blur Detection](https://arxiv.org/pdf/2006.03182.pdf) by Fan Yang and Xiao Xiao. Please visit the MSDU-Net paper for more detail.
Possibly, there are mistakes in the implementation. I do not guarantee the exact accuracy/performance claimed in the paper. I want to share my understanding and model after reading this paper.

# Model
It consists of 4 extractors, which use dilated convolutions, in front of the UNet. Each extractor gets the same input image but feeds its output to a different level of the UNet. Please look at the figures inside the paper for greater detail.
![Model's architecture](/images/msdu-net.png)

## Dataset
I trained the model from a combined dataset between CUHK and DUT for blur detection. 
CUHK contains both motion-blurred images and defocused images. I split the data into training and test sets (800 training, 200 test) in a way that preserved the ratio between two kinds of blurs.
DUT contains both training and test sets (600 training, 500 test) split by the authors. I converted files from .bmp to .png and inverted the black/white color in the masks. Please consult these datasets for more detail.


The new dataset consists of 1400 pairs of images and ground truth images as a training set and 700 pairs as a test set.
![Example of the input image](/dataset/Training/image/505.jpg)
![Example of the ground truth image](/dataset/Training/gt/505.png)

## Hyperparameters
My input images are of 128x128 RGB images with 128x128 1-channel grayscale ground truth masks.
1. learning rate is 0.01
2. momentum is 0.9
3. weight_decay is 5e-4
4. batch_size is 16
5. epochs are 100
These values are set as described in the paper. I have not explored different sets of hyperparameters yet.

## Performance
The results I got seem decent enough. But they are not quite as good as presented in the paper, which makes me believe that my implementation has something wrong with it still.
Here are some comparisons between the input image, the predicted mask, and the ground truth mask.
![Results](/images/result_example.jpg)
Also, I have not compared the proposed architecture to different architectures yet.
In the paper, the author proposed much better metrics to compare the performance of this architecture to the others.

The graph of the training-test losses and accuracies may not make much sense. But here it is.
![Losses and accuracies](/images/losses_and_accuracies.png)

## My machine
The model was trained using Nvidia RTX 3070 with 8 GB of memory. It took around 45 minutes to finish the training process.

## Reflection
This repo is the first time I tried to implement a model following a paper on my own. I did not know about the image segmentation, UNet, dilated convolutions, weight_decay, and learning_rate scheduler before. It was a great learning experience!