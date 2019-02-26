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


