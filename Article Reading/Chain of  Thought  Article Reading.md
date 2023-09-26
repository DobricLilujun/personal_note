# Graph of  Thought  

## Background

Human thinking is often characterized by its ability to make sudden leaps and connections between seemingly unrelated ideas, which can lead to novel insights and solutions.

**Structure-Aware Abstractive Conversation Summarization via Discourse and Action Graphs**

Discourse relation types 

We first pre-train a discourse
parsing model (Shi and Huang, 2019) on a human-
annotated multiparty dialogue corpus

Pre-trained parser

通过模型去量化多重不同对话之间的关系，建立对话关系图，并进一步建立who does what的动作图来进行对话关键信息的提取

**Leveraging Linguistic Structure For Open Domain Information Extraction**

从长句中提取独立子句并转化为关系三元组的方法



## Main article

该文章提出了一种思想图的模型来增加大预言模型在逻辑问题处理方向的优化和加强.其模型输入为OpenIE系统所输出的句子的三元组并进行ECC过程,也就是通过每一句话内部的主谓关系来进行基本thought的生成以及进行共同推断思想单元的整理. 也就是简单来说,也就是分解句子得到元想法,并对原想法去构建图.

而其也加入了原句子,额外的图片等等输入到endoer模型中进行编码,其具体架构如下所示.

![](C:\Users\lujun.li\OneDrive - University of Luxembourg\Bureau\Random\personal_note\Article Reading\Chain of  Thought  Article Reading.assets\GOT-1695729601747-2.PNG)







