# Using Transfer Learning and MobileNet to build an Alpaca Classifier

## Explaining MobileNet

MobileNet is a convolutional neural network(CNN) architecture designed for low compute environments
e.g mobile phones or embedded systems.

The MobileNet paper: <b>MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications</b> can be found here: https://www.researchgate.net/publication/316184205_MobileNets_Efficient_Convolutional_Neural_Networks_for_Mobile_Vision_Applications

The key aspect of MobileNet is that it uses Depthwise-Seperable Convolutions as opposed to Normal Convolutions.

Normal Convolutions can be thought of as volumetric where you multiply volumes to volumes.
![Normal Convolution](images/Normal_Convolution.PNG)

<br>
Depthwise-Seperable Convolutions are broken into Depthwise and then seperable convolutions

### Depthwise
This involves convolutions per single channel e.g depth.
Here, e.g channel has it's own filter. Red convolved with red filter and so on..
![Depthwise Convolution](images/Depthwise.PNG)

### Seperable(Pointwise)
The output of the depthwise part is then convolved with a number of 1x1 filters. The number of filters 
is equal to desired number of channels in the final output.
![Seperable Convolution](images/Pointwise_Convolution.PNG)

## Why MobileNet works

The number of multiplications(computational cost) needed to achieve the same output as normal convolutions is significantly less when using Depthwise-Seperable convolutions.
This makes it very useful in system which don't have a lot of computaional power.

## What about Accuracy

MobileNet does not sacrifice accuracy inorder to achieve low computational cost. Below is a table comparing
it to other popular networks such as the inception network from GoogleNet and VGG-16
![Comparison](images/MobileNet_Comparison.PNG)