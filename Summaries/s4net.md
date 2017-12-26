S4Net: Single Stage Salient-Instance Segmentation.
https://arxiv.org/pdf/1711.07618.pdf

It's like mask rcnn but for salient instances. 

I don't think the paper gives enough information to recreate the net, so probably not that much to learn from it atm. Added the github page to my watchlist for when they release the TF code.

Abstract:
> In this paper, we consider an interesting vision
problem—salient instance segmentation. Other than producing
approximate bounding boxes, our network also outputs
high-quality instance-level segments. Taking into account
the category-independent property of each target, we
design a single stage salient instance segmentation framework,
with a novel segmentation branch. Our new branch
regards not only local context inside each detection window
but also its surrounding context, enabling us to distinguish
the instances in the same scope even with obstruction.
Our network is end-to-end trainable and runs at a
fast speed (40 fps when processing an image with resolution
320 × 320). We evaluate our approach on a public
available benchmark and show that it outperforms other alternative
solutions. In addition, we also provide a thorough
analysis of the design choices to help readers better understand
the functions of each part in our network. To facilitate
the development of this area, our code will be available at
https://github.com/RuochenFan/S4Net.

They invented a layer "mask pooling" that they claim is better than ROI pooling and ROI align.

>As can be seen, our proposed
binary RoIMasking and ternary RoIMasking both outperform
RoIPool and RoIAlign in mAP0.7
. Specifically, our
ternary RoIMasking result improves the RoIAlign result by
around 2.5 points. This reflects that considering more context
information outside the proposals does help for salient
instance segmentation


Important benchmark IMO:

![s4net speed benchmark](../Assets/s4net_benchmark.png?raw=true "s4net_benchmark")
