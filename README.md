## 2019-2-18
### Integrated unpaired appearance-preserving shape translation across domains <br>
- 这篇文章做的是自动试衣/脱衣系统。试衣：给定一个人和一件衣服，输出这个人同样姿态下穿上这个衣服的照片。脱衣：输入照片为一个人，输出这个人的衣服的标准照片。\[[pdf](https://arxiv.org/pdf/1812.02134.pdf)\]

### A Style-Based Generator Architecture for Generative Adversarial Networks <br>
- 人称GAN2.0。通过风格迁移里的AdaIN的概念重新定义了生成器架构，可以自动实现概念层面的解耦，以及生成微小的variance。\[[pdf](https://arxiv.org/abs/1812.04948)\]

### DocFace: Matching ID Document Photo to Selfies
- 人证核验场景。训练数据为证件照和现场照pair，关注domain的不同。使用sibling网络分别提取不同domain的特征，提出对应的损失函数。\[[pdf](https://arxiv.org/pdf/1805.02283.pdf)]

### Spatial Transformer Networks
- CNN可以显示的学习平移不变性，隐式的学习到对旋转，伸缩、尺度等变换的不变性，Google  DeepMind 2016年提出的STN网络，可以显式地赋予网络对上述变换的不变性。不依赖于关键点进行矫正和对齐，而且网络可以作为模块加入神经网络的各个层中。\[[pdf](https://arxiv.org/abs/1506.02025)]

### GridFace: Face Rectication via Learning Local Homography Transformations
- 旷视识别组老大周而进ECCV2018的一篇论文，通过grid-stn将人脸分成网格学习局部单应变换，结合自然人脸分布的正则化，可以提升人脸对齐的效果，用在训练中可以涨点，值得一看。\[[pdf](https://arxiv.org/abs/1808.06210)]

## 2019-2-25

### Cross-spectral Face Completion for NIR-VIS Heterogeneous Face Recognition
- 这是一篇异构人脸识别的文章，通过将近红外图像转换成可见光图像，实现在同一个域下进行人脸识别。具体做法是将高分辨率的人脸合成简化成两个组件：纹理修复组件（从NIR域迁移至VIS域）和pose矫正组件（保证迁移最后生成的可见光图像是正脸）；之后通过一个Warping Net进行整合，输出一个目标合成可见光正脸图像。整体思想还是GAN的思想，对D做了一些改进。\[[pdf](https://arxiv.org/abs/1902.03565)]
- 异构人脸识别主要有以下几种方法：

	1. 基于图像合成的方法，从一个域迁移到另一个域，和本文中心思想一致，作者在列举了一大堆现有方法之后，提出现有的异构人脸域迁移还不能输出高分辨率的图像，因为NIR图像的背景一般是截断的。
	2. 基于潜在子空间迁移的方法，投影两个不同模组的数据到共同的潜在子空间，这个子空间可以度量异构数据的相关性。
	3. 训练域不变性feature，将ID信息与其他的域信息解耦出来，通常做法是在一个比较大规模的VIS数据集上训练，然后在NIR数据集上fine-tune，从而学习domain-invariant features

### Why do deep convolutional networks generalize so poorly to small image transformations?
- 这篇文章提出，对图像中object进行微小的缩放或者平移，一个CNN图像分类器可能就会从认识object变得不认识object。文章提出，这是因为当代CNN忽略了采样定理(如果按照下采样比例同样的大小像素数移动object，则会有平移不变性)，以及训练数据集的bias。分析的比较到位。 \[[pdf](https://arxiv.org/abs/1805.12177)]

### Self-Attention Generative Adversarial Networks
- 借助Xiaolong Wang的Non-local文章中的思想，在GAN的生成器和判别器中施加Self-Attention去强制网络关注object的整体结构，而不是受传统CNN的限制，只关注局部特征。\[[pdf](https://arxiv.org/abs/1805.08318)]

### SC-FEGAN:Face Editing Generative Adversarial Network with User's Sketch and Color
- 一个基于GAN的人脸图片编辑系统。对于一张人脸图片，用户擦去一部分并提供对应轮廓草图和颜色信息，该系统生成一定程度符合用户期望的完整图片。生成器使用了U-net结构，结合与用户输入相关的信息提供额外先验，判别器使用了SN-PatchGAN结构对图像patch分别判定，额外的style loss保证生成图像的合理性。文章给出了完整对训练数据的制作方式，能够产生大量的训练样本，使用了一些小的技巧，确保生成器只关注缺失部分的生成。设计比较巧妙，从文章给出的结果来看图像编辑效果卓越。\[[pdf](https://arxiv.org/abs/1902.06838)]

## 2019-03-04
### RGB-based 3D Hand Pose Estimation via Privileged Learning with Depth Images
- 背景：

	深度图数据更干净更多，最后的准确率也高很多，而RGB的就要差很远，

	但是实际应用的时候，大部分只有RGB的图，所以想到用预训练的深度图训练出来的网络去教RGB网络，这样应该能得到更好的效果。

	这样在测试的时候就不用深度图，只用RGB就行。

	大体思路：

	1、在深度图数据训练一个基于深度图的网络，然后在一个另一个有RGB配对的数据集上用深度图finetune

	2、在配对数据集上用RGB训练一个网络

	3、在配对数据集上用RGB结合深度图，锁定深度数据图，通过Loss_inter来联合训练RGB网络。Loss_inter其实就是特征层的MSE。

	\[[pdf](https://arxiv.org/abs/1811.07376)]

### Multi-Prototype Networks for Unconstrained Set-based Face Recognition
- 论文解决的是非约束场景的人脸识别问题，和主流基于单张人脸图像识别训练的pipeline不同的是：训练阶段基于集合的，且不做2D或者3D的align，集合里面包含R张（R是个超参数）当前ID的图像，利用稠密子图学习方法（Dense SubGraph learning）encoding不同的光照、年龄、等属性信息，最后通过降维可视化验证了文章提出的dense subgraph learning的方法在属性聚类方面的有效性，并提升了非约束场景人脸识别指定far下的recall。\[[pdf](https://arxiv.org/pdf/1902.04755v3.pdf)]

## 2019-03-11
### Region Proposal by Guided Anchoring
- 常规的faster rcnn目标检测系统通常需要固定的anchor来生成proposals，这篇文章指出anchor的大小和位置可以让网络自主学习，这样的学习过程通过end2end的方式能提高AR将近10个百分点。具体而言是在RPN的feature顶端加上center prediction和w,h prediction来生成anchor。\[[pdf](https://arxiv.org/abs/1901.03278)]

### SCALABLE FACIAL IMAGE COMPRESSION WITH DEEP FEATURE RECONSTRUCTION
- 本文提出了一种可扩展的图像压缩方案，包括用于特征表示的基础层以及用于纹理表示的增强层，充分的利用了CTA（compress-then-analyze）和ATC（analyze-then-compress）各自的优势。
注：
CTA（compress-then-analyze）：监控场景的数据从前端压缩并传递到后端，然后再执行分析任务，目前使用低bit压缩量化，解码出的图像质量较差，因此提出的特征也比较差。
ATC（analyze-then-compress）：直接在前端完成特征提取、压缩和传输，这样前端提取的压缩特征就可以传输到服务器端，由于特征比纹理更紧凑，分析任务的性能在低比特率下非常有前途。\[[pdf](https://arxiv.org/pdf/1903.05921.pdf)]

### Dynamic Curriculum Learning for Imbalanced Data Classification
- 本文针对人的属性分析中训练样本分布不均衡的问题，提出了 Dynamic Curriculum Learning(DCL)，可以自适应的改变每个minibatch中的采样策略和loss反向传播的比例，提升了泛化性能和辨别性。

DCL主要分为两级课程调度表 two-level curriculum schedulers（不知这么翻译对不对）

1. sampling scheduler:
管理采样的数据分布，从不平衡的数据分布到均衡，数据分布也由易到难；

2. loss scheduler 控制分类和度量学习损失的重要性。\[[pdf](https://arxiv.org/abs/1901.06783)]
