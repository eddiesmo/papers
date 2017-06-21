
Learning the architecture and tricks of inception networks across generations.
The following 3 sources link to the relevant papers and summarize the history. 


- http://nicolovaligi.com/history-inception-deep-learning-architecture.html
- http://davidstutz.de/going-deeper-with-convolutions-szegedy-et-al/
- http://davidstutz.de/rethinking-the-inception-architecture-for-computer-vision-szegedy-et-al/
    
The actual papers:

(the notes are mainly for myself)

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
https://arxiv.org/pdf/1512.00567v3.pdf

This paper explains the thinking behind GoogLeNet and improves upon it. 
Many engineering improvements have been added and accumulated to a 50% 
decrease in the top-5 error on imagenet. 

Abstract:
> Convolutional networks are at the core of most stateof-the-art
computer vision solutions for a wide variety of
tasks. Since 2014 very deep convolutional networks started
to become mainstream, yielding substantial gains in various
benchmarks. Although increased model size and computational
cost tend to translate to immediate quality gains
for most tasks (as long as enough labeled data is provided
for training), computational efficiency and low parameter
count are still enabling factors for various use cases such as
mobile vision and big-data scenarios. Here we are exploring
ways to scale up networks in ways that aim at utilizing
the added computation as efficiently as possible by suitably
factorized convolutions and aggressive regularization. We
benchmark our methods on the ILSVRC 2012 classification
challenge validation set demonstrate substantial gains over
the state of the art: 21.2% top-1 and 5.6% top-5 error for
single frame evaluation using a network with a computational
cost of 5 billion multiply-adds per inference and with
using less than 25 million parameters. With an ensemble of
4 models and multi-crop evaluation, we report 3.5% top-5
error and 17.3% top-1 error.

From the intro: 
> In this paper, we start with describing a few
general principles and optimization ideas that that proved
to be useful for scaling up convolution networks in efficient
ways. Although our principles are not limited to Inceptiontype
networks, they are easier to observe in that context as
the generic structure of the Inception style building blocks
is flexible enough to incorporate those constraints naturally.
This is enabled by the generous use of dimensional reduction
and parallel structures of the Inception modules which
allows for mitigating the impact of structural changes on
nearby components.

GoogLeNet is light on params:

>  GoogleNet employed only 5 million parameters, which
represented a 12× reduction with respect to its predecessor
AlexNet, which used 60 million parameters. Furthermore,
VGGNet employed about 3x more parameters than AlexNet

GoogLeNet is complicated:

> Still, the complexity of the Inception architecture makes
it more difficult to make changes to the network. If the architecture
is scaled up naively, large parts of the computational
gains can be immediately lost.

The `General Design Principles` section is very interesting and worth reading in its entirety. 

The sections `Factorization into smaller convolutions` and 
`Spatial Factorization into Asymmetric Convolutions` discuss reducing the 
filter parameter count and computation amount. 
Simple tricks that bring ~30% reductions each. 

re: spatial factorization: 
> In practice, we have found that employing this factorization
does not work well on early layers, but it gives very good results
on medium grid-sizes (On m×m feature maps, where
m ranges between 12 and 20). On that level, very good results
can be achieved by using 1 × 7 convolutions followed
by 7 × 1 convolutions.

Auxiliary classifiers:

> [20] has introduced the notion of auxiliary classifiers to
improve the convergence of very deep networks. The original
motivation was to push useful gradients to the lower layers
to make them immediately useful and improve the convergence
during training by combating the vanishing gradient
problem in very deep networks. Also Lee et al[11]
argues that auxiliary classifiers promote more stable learning
and better convergence. Interestingly, we found that
auxiliary classifiers did not result in improved convergence
early in the training: the training progression of network
with and without side head looks virtually identical before
both models reach high accuracy. Near the end of training,
the network with the auxiliary branches starts to overtake
the accuracy of the network without any auxiliary branch
and reaches a slightly higher plateau.

> [...] Instead, we argue that the auxiliary classifiers
act as regularizer. This is supported by the fact that
the main classifier of the network performs better if the side
branch is batch-normalized [7] or has a dropout layer. This
also gives a weak supporting evidence for the conjecture
that batch normalization acts as a regularizer.

Inception V2: 

> Although our network [inception v2] is 42 layers deep, our computation cost is only about 2.5 higher
than that of GoogLeNet and it is still much more efficient
than VGGNet.

Thoughts:
the net goes down to a small activation grid very fast (from 299 to ~35) and 
does most of the computations there. I wonder how this affects spatial, 
pixel-level nets that deal with e.g. edge detection or segmentation.

I didn't fully grok the section: `Model Regularization via Label Smoothing` but it only reduced the error rate by 0.2% so not very important.

Training Methodology:

> We have trained our networks with stochastic gradient
utilizing the TensorFlow [1] distributed machine learning
system using 50 replicas running each on a NVidia Kepler
GPU with batch size 32 for 100 epochs. Our earlier experiments
used momentum [19] with a decay of 0.9, while our
best models were achieved using RMSProp [21] with decay
of 0.9 and  = 1.0. We used a learning rate of 0.045,
decayed every two epoch using an exponential rate of 0.94.
In addition, gradient clipping [14] with threshold 2.0 was
found to be useful to stabilize the training. Model evaluations
are performed using a running average of the parameters
computed over time.

# Inception-v4, Inception-ResNet and
the Impact of Residual Connections on Learning
https://arxiv.org/pdf/1602.07261v2.pdf

[Skimmed]