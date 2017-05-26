# Paper
* **Title**: The Do’s and Don’ts for CNN-based Face Verification
* **Authors**: Ankan Bansal Carlos Castillo Rajeev Ranjan Rama Chellappa
UMIACS - 
University of Maryland, College Park
* **Link**: https://arxiv.org/abs/1705.07426

# Abstract
>Convolutional neural networks (CNN) have become the most sought after tools for addressing object recognition problems. Specifically, they have produced state-of-the art results for unconstrained face recognition and verification tasks. While the research community appears to have developed a consensus on the methods of acquiring annotated data, design and training of CNNs, many questions still remain to be answered. In this paper, we explore the following questions that are critical to face recognition research: (i) Can we train on still images and expect the systems to work on videos? (ii) Are deeper datasets better than wider datasets? (iii) Does adding label noise lead to improvement in performance of deep networks? (iv) Is alignment needed for face recognition? We address these questions by training CNNs using CASIA-WebFace, UMDFaces, and a new video dataset and testing on YouTubeFaces, IJBA and a disjoint portion of UMDFaces datasets. Our new data set, which will be made publicly available, has 22,075 videos and 3,735,476 human annotated frames extracted from them.

# How they made the dataset
- collect youtube videos
- automated filtering with yolo and landmark detection projects
- crowd source final filtering (AMT - give 50 face images to turks and ask which don't belong)
- quality control through sentinels: give turks the same test but with 5 known correct answers, 
and rank the turks according to how they perform on this ground truth test. 
If they're good, trust their answers on the real tests.
- result: 
    > we have 3,735,476 annotated frames in 22,075 videos. We will
    publicly release this massive dataset
# Introduction
>We make the following main contributions in this paper:
• We introduce a large dataset of videos of over
3,000 subjects along with 3,735,476 human annotated
bounding boxes in frames extracted from these videos.
• We conduct a large scale systematic study about the
effects of making certain apparently routine decisions
about the training procedure. Our experiments clearly
show that data variety, number of individuals in the
dataset, quality of the dataset, and good alignment are
keys to obtaining good performance.
• We suggest the best practices that could lead to an improvement
in the performance of deep face recognition
networks. These practices will also guide future data
collection efforts.

# Questions and experiments
## Do deep recognition networks trained on stills perform well on videos?
> We study the effects of this difference between
still images and frames extracted from videos in section
3.1 using our new dataset. We found that mixing both
still images and the large number of video frames during
training performs better than using just still images or video
frames for testing on any of the test datasets
## What is better: deeper or wider datasets?
>In section 3.2 we investigate the impact of using a deep
dataset against using a wider dataset. For two datasets with
the same number of images, we call one deeper than the
other if on average it has more images per subject (and
hence fewer subjects) than the other. We show that it is
important to have a wider dataset than a deeper dataset with
the same number of images.

## Does some amount of label noise help improve
the performance of deep recognition
networks?
>When training any supervised face classification system,
each image is first associated with a label. Label noise is the
phenomenon of assigning an incorrect label to some images.
Label noise is an inherent part of the data collection process.
Some authors intentionally leave in some label noise [25, 6,
7] in the dataset in hopes of making the deep networks more
robust. In section 3.3 we examine the effect of this label
noise on the performance of deep networks for verification
trained on these datasets and demonstrate that clean datasets
almost always lead to significantly better performance than
noisy datasets.

## Does thumbnail creation method affect performance?
>... This leads to generation of different types
of bounding boxes for faces. Verification accuracy can
be affected by the type of bounding box used. In addition,
most recent face recognition and verification methods
[35, 31, 33, 5, 9, 34] use some kind of 2D or 3D alignment
procedure [41, 14, 28, 8]. ... In section 3.4 we study the consequences
of using different thumbnail generation methods
on verification performance of deep networks. We show
that using a good keypoint detection method and aligning
faces both during training and testing leads to the best performance.

