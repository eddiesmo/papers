
Learning the architecture and tricks of inception networks across generations.
The following 3 sources link to the relevant papers and summarize the history. 


- http://nicolovaligi.com/history-inception-deep-learning-architecture.html
- http://davidstutz.de/going-deeper-with-convolutions-szegedy-et-al/
- http://davidstutz.de/rethinking-the-inception-architecture-for-computer-vision-szegedy-et-al/
    
The actual papers:

# Network In Network
https://arxiv.org/pdf/1312.4400v3.pdf
    
> We propose a novel deep network structure called “Network In Network”(NIN)
to enhance model discriminability for local patches within the receptive field. The
conventional convolutional layer uses linear filters followed by a nonlinear activation
function to scan the input. Instead, we build micro neural networks with
more complex structures to abstract the data within the receptive field. We instantiate
the micro neural network with a multilayer perceptron, which is a potent
function approximator. **The feature maps are obtained by sliding the micro networks
over the input in a similar manner as CNN; they are then fed into the next
layer. Deep NIN can be implemented by stacking mutiple of the above described
structure.** With enhanced local modeling via the micro network, we are able to utilize
global average pooling over feature maps in the classification layer, which is
easier to interpret and less prone to overfitting than traditional fully connected layers.
We demonstrated the state-of-the-art classification performances with NIN on
CIFAR-10 and CIFAR-100, and reasonable performances on SVHN and MNIST
datasets

# Going deeper with convolutions
https://arxiv.org/pdf/1409.4842v1.pdf

Abstract:

> We propose a deep convolutional neural network architecture codenamed Inception,
which was responsible for setting the new state of the art for classification
and detection in the ImageNet Large-Scale Visual Recognition Challenge 2014
(ILSVRC14). The main hallmark of this architecture is the improved utilization
of the computing resources inside the network. This was achieved by a carefully
crafted design that allows for increasing the depth and width of the network while
keeping the computational budget constant. To optimize quality, the architectural
decisions were based on the Hebbian principle and the intuition of multi-scale
processing. One particular incarnation used in our submission for ILSVRC14 is
called GoogLeNet, a 22 layers deep network, the quality of which is assessed in
the context of classification and detection.

A very interesting paper to read. Lots of insight and discussion. 
I enjoyed section 6: "Training Methodology", where it's apparent that even 
Google sometimes does things in a hurry and doesn't fully document their 
experiments :)

> [...] so we could not tell definitely whether the final results were affected positively by their
use [...]

> These models were trained with the same initialization 
(even with the same initial weights, mainly because of an oversight) [...]

Inception is light on parameters: 
> Our GoogLeNet submission to ILSVRC 2014 actually uses 12× fewer parameters
than the winning architecture of Krizhevsky et al [9] from two years ago, while being significantly
more accurate.

Memes:
> In this paper, we will focus on an efficient deep neural network architecture for computer vision,
codenamed Inception, which derives its name from the Network in network paper by Lin et al [12]
in conjunction with the famous **“we need to go deeper” internet meme** [1].

Auxiliary networks:

> Given the relatively large depth of the network, the ability to propagate gradients back through all the
layers in an effective manner was a concern. One interesting insight is that the strong performance
of relatively shallower networks on this task suggests that the features produced by the layers in the
middle of the network should be very discriminative. By adding auxiliary classifiers connected to
these intermediate layers, we would expect to encourage discrimination in the lower stages in the
classifier, increase the gradient signal that gets propagated back, and provide additional regularization.
These classifiers take the form of smaller convolutional networks put on top of the output of
the Inception (4a) and (4d) modules. During training, their loss gets added to the total loss of the
network with a discount weight (the losses of the auxiliary classifiers were weighted by 0.3). At
inference time, these auxiliary networks are discarded.

Note to self: The auxiliary networks are a form of deep supervision 
(See skip connections in the HED edge detection paper).

Testing techniques:
- GoogLeNet with 1 model (no ensemble) and no crops: 10.07% top-5 error.
- GoogLeNet with 7 models ensemble and 144 crops: 6.67% top-5 error.


Open questions:
- Understand the numbers of 1x1 convolutions and the exact architecture of each inception module


# Rethinking the Inception Architecture for Computer Vision
[TO DO]
https://arxiv.org/pdf/1512.00567v3.pdf
