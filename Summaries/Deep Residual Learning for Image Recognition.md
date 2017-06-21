Learning about Resnet with an eye for segmentation tasks.

The researchers:
> Kaiming He with Xiangyu Zhang, Shaoqing Ren, Jifeng Dai, & Jian Sun
 -- Microsoft Research Asia (MSRA)

# Deep Residual Learning for Image Recognition
Sources:
- https://arxiv.org/pdf/1512.03385.pdf
- http://image-net.org/challenges/talks/ilsvrc2015_deep_residual_learning_kaiminghe.pdf

Sumary:
- Took the first place in Imagenet 5 main tracks
- Revolution of depth: GoogLeNet was 22 layers with 6.7 top-5 error, 
Resnet is 152 layers with 3.57 top-5 error
- Light on complexity: the 34 layer baseline is 18% of the FLOPs(multiply-adds) of VGG.
    - Resnet 152 has lower time complexity than VGG-16/19
- Extends well to detection and segmentation tasks
- Just stacking more layers gives worse performance. Why? In theory:
    > A deeper model should not have
    higher training error
    • A solution by construction:
    • original layers: copied from a
    learned shallower model
    • extra layers: set as identity
    • at least the same training error
    • Optimization difficulties: solvers
    cannot find the solution when going
    deeper…
- Why do the residual connections help? it's easier to learn a residual mapping w.r.t. identity. 
    - If identity were optimal, easy to set weights as 0
    - >If the optimal function is closer to an identity
mapping than to a zero mapping, it should be easier for the
solver to find the perturbations with reference to an identity
mapping, than to learn the function as a new one. We show
by experiments (Fig. 7) that the learned residual functions in
general have small responses, suggesting that identity mappings
provide reasonable preconditioning.
- Basic design (VGG-style)
    - all 3x3 conv (almost)
    - spatial size /2 => # filters x2
    - Simple design; just deep!
    - Other remarks:
        - no max pooling (almost)
        - no hidden fc
        - no dropout
- Training
    - All plain/residual nets are trained from scratch
    - All plain/residual nets use Batch Normalization
    - Standard hyper-parameters & augmentation
- The learned features are well transferable to other tasks
    - Works well with Faster RCNN
    - Works well with semantic instance segmentation
 

Also skimmed:
- Deep Residual Networks with 1K Layers
https://github.com/KaimingHe/resnet-1k-layers 
https://arxiv.org/pdf/1603.05027.pdf
