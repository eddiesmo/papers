# Visual Object Segmentation with Reidentification 
- The optical flow doesn't add a lot
- Uses many different nets 
    - mask propagation net with two streams
    - detection net (Faster R-CNN)
    - identification net 
        > (T. Xiao, S. Li, B.Wang, L. Lin, and X.Wang. Joint detection
and identification feature learning for person search. In
CVPR, 2017)
- Has a backwards and forward pass for the re-identification so probably bad runtime
- Upgrades over lucid Dream:
    - Full image to bounding box is a good upgrade over Lucid Dream (adds ~4%)
    - Based on resnet and not vgg16
    - other tricks: atrous spatial pyramid pooling and multi-scale testing
- What is multiscale testing?

# Lucid Data Dreaming for Object Tracking
Risks and thoughts:
In our case:
- Low fps, big jumps between frames
- Small movement between foreground and background

Will the optical flow and mask tracking be as effective? 
> Comparing our full system to the
"No OF" row, we see that the effect of optical flow varies
across datasets, from minor improvement in YouTubeObjects,
to major difference in SegTrackv2.

Speed:
> It takes ~3.5h to obtain each per-video model, including
data generation, per-dataset training, per-video fine-tuning
and per-dataset grid search of CRF parameters (averaged
over DAVIS, amortizing the training time over all videos).
At test time our LucidTracker runs at ~5s per frame, including
the optical flow computation with FlowNet2.0 [20]
(~0.5s) and CRF post-processing [26] (~2s)


# Instance Re-Identification for Video Object Segmentation
> For each video frame, we localize the.     instances in a reidentification
manner. For human instances, we first detect
person from the image by using Faster R-CNN [16]. Then,
we extract person re-identification feature [19] for all detected
person region. For the implementation, we use the
state-of-the-art implementation to detect1
and extract person
re-identification feature2
. DeepFlow and Deformable
Part Models (DPM) [4] are utilized to track and detect nonhuman
objects.

re-identification is less relevant for the GyGO dataset.


# Multiple-Instance Video Segmentation with Sequence-Specific Object Proposals