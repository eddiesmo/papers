Learning about Resnet with an eye for segmentation tasks.

The researchers:
> Kaiming He with Xiangyu Zhang, Shaoqing Ren, Jifeng Dai, & Jian Sun
 -- Microsoft Research Asia (MSRA)

# Deep Residual Learning Presentation in ICCV
http://image-net.org/challenges/talks/ilsvrc2015_deep_residual_learning_kaiminghe.pdf
- Took the first place in Imagenet 5 main tracks
- Revolution of depth: GoogLeNet was 22 layers with 6.7 top-5 error, 
Resnet is 152 layers with 3.57 top-5 error
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
    - If optimal mapping is closer to identity, easier to find small fluctuations
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
- Resnet 152 has lower time complexity than VGG-16/19
- The learned features are well transferable to other tasks
    - Works well with Faster RCNN
    - Works well with semantic instance segmentation

 
# Questions
 - How did researchers "see" the weak gradients in vanilla deep nets? How did they recognize the problem?
 -  
  
