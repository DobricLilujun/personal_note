# Content



在微观的研究中，很多的物理系统是时间可逆的，因为我们能够直接研究组成物理系统的最小微粒。但是在宏观系统中，很多物理系统便不再是时间可逆的，因为我们只能得到宏观系统的一些统计物理量，而这种信息获取其实本质上丢失了很多信息。而下面的实验主要研究在宏观尺度下，如果能够得知在终止状态的前提下，得到起始状态，间接找回所丢失的核心信息。In microscopic studies, many physical systems are time-reversible because we can directly investigate the smallest particles composing the physical system. However, in macroscopic systems, many physical systems cease to be time-reversible, as we can only obtain some statistical physical quantities of the macroscopic system. This information retrieval essentially loses a considerable amount of information. The following experiment primarily explores, at the macroscopic scale, the possibility of obtaining the initial state under the condition of knowing the final state, thereby indirectly recovering the lost core information.



Diffusion based approach is mostly used in recent years and it's already been used in the previous diffusion model. And the article discussed in the previous section shows the equivalence of diffusion approach and score matching approach. In general:

First of all, for a stochastic differential equation (SDE)

dx = f(x,t) dt + g(t)dW

简单地来说，我们研究的物理模型可以被描述为：

其中 P （x）是物理模型中确定性的部分，称之为drift，而g(x)则称之为diffusion,即所有的随机性的部分。而在下面的模型中，确定性的部分P（x）的正向和反向过程P-1是已知的。



SDE可被视为[动力系统理论](https://zh.wikipedia.org/wiki/动力系统理论)对有噪模型的一种概括





理论上来说，以我的理解，对于分数的定义就是对数据分布的导数 delta log pt_x。那么如果对于一个模型，如果我知道这个分数score，SDE可以在时间上反向。而这个分数，是在这个时间t上，更加高维度的数据分布p(x)的描述。而和之前不同的是，对于diffusion model来说，它主要是讲数据从基本的数据分布逐渐转化为噪音。而对于现在的物理问题的反问题，其研究的是物理的状态变化。因此它选择了初始状态和终止状态，当然也需要高斯噪声来作为干扰。而最终，这个分数会通过一个神经网络去逼近，来得到最终的分数，而这个分数也是可逆的。

总之，在物理系统的反问题中，我们可以通过采样正问题来学习分数score，通过这个分数来，给定最终时刻的状态，这个模型来逐步预测前时刻的状态。这个过程与扩散模型中的去噪过程类似。



根据其中的定理3.1,我们可以得出，如果根据SDE我们采样出的轨迹的数据集，那么以1-step loss 的训练可以等价为一score matching 问题，也就是最小化目标函数的问题。



L_jump(theta)



优点：

首先扩散模型的建模效果好，能够准确地建模数据分布。其次扩散模型的损失函数构建特别简单，训练特别稳定。

扩散模型除了可以看作是MHVAE之外，甚至还可以看作是能量模型（EBM），连续正则化流（CNF）的特殊形式。



1. 拟合数据分布最常见的做法就是最大似然估计。如果将建模的数据分布写成更加通用的能量模型形式，如何计算能量模型的配分函数Z是一个巨大问题。

2. Score-matching的方法就是一个最好的办法。我们可以通过估计对输入x的梯度（称为score）来实现MCMC的游走采样，从而计算scroe。 

3. 有了score就可以通过朗之万动力学采样的方式近似从P_theta里采样。

4. 将能量模型建模为score，即用一个神经网络来你和score。

   困难1：遇到低维流形的问题，也就是希望拟合的数据在高维空间里表现为低维流形，那么对零概率的空间点取对数毫无意义

   困难2：score matching 的优化目标是个L2范数的期望， 对于低密度的区域，无法得到足够多的样本来进行监督训练

5. 上述的问题在数据中添加高斯噪声解决，因为高斯噪声定义在整个参数域，且低概率区也可以得到更多信号。

6. 构建扩散过程，对不同尺度的噪声的L2 范数进行加权求和。DDPM的训练目标完全等价于扩散过程下的score matching 的训练目标

7. SDE的逆向过程也是一个SDE。DDPM找到对应于逆向SDE，且存在对应的ODE形式。ODE则最后可以用于采样加速，因为其连续的形式更加会加速采样。





根据我对于SDE逆向过程的理解，我们总结了如下的图来构建DDPM,SDE,ODE以及score mathing之间的联系，请根据关系图来理解这些模型之间的关系。



According to my understanding of the SDE reverse process, we have summarized the following diagram to establish connections between DDPM, SDE, ODE, and score matching. Please refer to the relationship diagram to understand the relationships between these models.

我们选择扩散模型首先是因为散模型的建模效果好，能够准确地建模数据分布。其次扩散模型的损失函数构建特别简单，训练特别稳定。而扩散模型最重要的目的就是拟合数据分布，比如说拟合出某类图像的像素点分布等等。



The choice of diffusion models is primarily due to their effective modeling, accurately capturing data distributions. Additionally, the loss function construction for diffusion models is notably simple, leading to stable training. The primary purpose of diffusion models is to fit data distributions, such as capturing pixel distributions in certain types of images.

首先，拟合数据分布最常见的做法就是最大似然估计。如果将建模的数据分布写成更加通用的能量模型形式，如何计算能量模型的配分函数Z是一个巨大问题。

The most common approach for fitting data distributions is maximum likelihood estimation. If we express the modeled data distribution in a more general energy model form, calculating the partition function Z for the energy model becomes a significant challenge.



然后我们有找到了Score-matching的方法，它就是一个最好的办法。我们可以通过估计对输入x的梯度（称为score）来实现MCMC的游走采样，从而计算scroe。



Subsequently, we have identified the Score-matching method, which proves to be an optimal solution. By estimating the gradient (referred to as the score) with respect to the input x, we can implement MCMC random walk sampling and compute the score.

再而有了score就可以通过朗之万动力学采样的方式近似从P_theta里采样。最后将能量模型建模为score，即用一个神经网络来拟合score。

With the score in hand, we can approximately sample from $\mathclr{P}_\theta$ using Langevin dynamics sampling. Finally, the energy model can be modeled as the score, utilizing a neural network to fit the score.



但是这种单一的score-matching 会遇到两个困难，困难1是训练会遇到低维流形的问题，也就是拟合的数据在高维空间里经常表现为低维流形，即对零概率的空间点取对数毫无意义。 困难2是score matching 的优化目标是个L2范数的期望， 对于低密度的区域，无法得到足够多的样本来进行监督训练。



However, this single Score-matching approach encounters two difficulties. The first difficulty is that training may face the problem of low-dimensional manifolds, where the fitted data often exhibits low-dimensional manifolds in high-dimensional space, rendering taking the logarithm of points in zero-probability spaces meaningless. The second difficulty is that the optimization objective of score matching is an L2 norm expectation, and for low-density regions, it is challenging to obtain enough samples for supervised training.



对于上述的问题，DDPM则通过在数据中添加高斯噪声解决，因为高斯噪声定义在整个参数域，且低概率区也可以得到更多信号。而构建所谓的扩散过程，其训练目标完全可以等价于SDE的score matching 的训练过程。而且ODE可以用于加速，也可以将SDE的score堪为离散化的ODE的形式



To address these issues, DDPM resolves them by adding Gaussian noise to the data, as Gaussian noise is defined over the entire parameter domain and provides more signals even in low-probability areas. Constructing the so-called diffusion process, its training objective is entirely equivalent to the score matching training process of SDE.

而在这种情况下，我们完全可以通过SDE求解器或者通过ODE求解器进行部分求解，从而于score matching联系。因为SDE的模拟与逆向过程需要score matching来进行近似。



In this scenario, we can use SDE solvers or ODE solvers for partial solutions, establishing a connection with score matching. This is because simulating SDE and the reverse engineering process both require approximations through score matching. It is also part of our research to use score matching methods in inverse problems in physics.
