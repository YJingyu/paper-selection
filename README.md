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
