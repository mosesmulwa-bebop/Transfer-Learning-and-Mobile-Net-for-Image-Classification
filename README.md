# Using Transfer Learning and MobileNet to build an Alpaca Classifier

## A. Explaining MobileNet

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
This makes it very useful in systems which don't have a lot of computaional power.

## What about Accuracy

MobileNet does not sacrifice accuracy inorder to achieve low computational cost. Below is a table comparing
it to other popular networks such as the inception network from GoogleNet and VGG-16.
<br>
![Comparison](images/MobileNet_Comparison.PNG)
<br>
Notice how it has relatively the same accuracy while having significantly less computational cost for training.


# B. Introducing MobileNet v2

MobileNetV2 is a convolutional neural network architecture that seeks to perform well on mobile devices. It is based on an inverted residual structure where the residual connections are between the bottleneck layers.
Paper: https://arxiv.org/abs/1801.04381v4

## A single block
<br>

![MobileNet v2](images/MobileNetv2.PNG)

<br>
It is similar to v1 except it uses skip connections too. It also adds an expansion layer before the depthwise
convolution.
The block is also called the <b>Bottleneck Block</b>
Expansion layer is comprised of a number of 1x1 filters whose number is greater than the channel size of the input.
This has the effect of increasing the number of channels.

## Why the bottleneck block works
Input to the block is expanded before the Convolution allowing network to learn a richer function. It is 
then projected down after convolution thereby reducing the memory needed to store the values. 
Thus it basically learns richer functions while only storing a small amount of values which are passed from layer to layer.


# C. Transfer Learning
Transfer learning allows us to use pre-trained networks and apply them to other use cases.
It basically involves replacing the final layers of the networks with our intended outputs. We then only train 
the new added layers.
All layers that came before are "frozen". 
Thus, we only train a small number of parameters as opposed to training the entire network.
We also get the added advantage of using a complex pre-trained network increasing our accuracy.


# D. Putting it all together


