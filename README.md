# 4x4-MIMO-prototype-system
This web page provides a 4x4 MIMO prototyping system in practical wireless MIMO communications. 

The prototyping implements important features of an orthogonal frequency division multiplexing (OFDM) physical layer, with third generation partnership project (3GPP) long-term evolution (LTE) time-division duplex (TDD)-like specifications.
* **Details about of the 4x4 MIMO prototype system** and **channel meaasurements** can refer to the  [4x4-MIMO-prototype-system.pdf](https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/4x4-MIMO-prototype-system.pdf). 
* **MIMO Channel Database** can be download from GoogleDrive [here](https://drive.google.com/file/d/1-eUTTWh8ZjWfEVatLC91Mi_Zp9zIGL76/view?usp=sharing).

## Table of Contents

- [Hardware Description](#hardware-description)
- [Phsical Layer Description](#phsical-layer-description)
- [MIMO Channel Measurements](#mimo-channel-measurements)
  - [Indoor-office measurements](#indoor-office-measurements)
  - [Indoor-hall measurements](#indoor-hall-measurements)
- [MIMO Channel Database](#mimo-channel-database)


## Hardware Description
<div align=center>
  <img src="https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/imag/hardware.jpg" width="50%" />
</div>
<div align=center>
Fig. 1. System hardware equipment overview.
</div>
To measure the channel characteristics of the MIMO channels,  4 universal software radio peripherals (USRP) are used to form a 4x4 MIMO prototyping system, which operating at 3.5GHz microwave band.  

Each USRP comprises two omni-directional antennas, two radio chains, and the respective ADC/DAC modules. It implements OFDM functionality such as (I)FFT  as well as digital front end functionality such as re-sampling on an FPGA. We use 4 antenna elements (2 USRPs) as the RX, thereby emulating a MIMO BS.  

Data arriving from the 4 antennas of BS is forward to the MIMO processors, which are implemented on a independent FPGA device in the PXI-Chassis. The FPGA device comprises MIMO processing operations such as precoding and equalization, as well as channel estimation in frequency domain. 

Two USRPs equipped with 4 antennas are used as transmitters, each USRP is connected with a controller computer. Note that a single USRP supports two antennas. It also supports the signal processing for two single antenna mobile stations which operate independently. Here we utilize 4 antennas to represent four independent users.


## Phsical Layer Description
The prototyping system implements parts of an LTE-like physical layer in TDD mode. Uplink and downlink are based on OFDM using 20 MHz channel bandwidth.

### Radio Frame Format
<div align=center>
  <img src="https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/imag/RadioFrame.jpg" width="50%" />
</div>
<div align=center>
Fig. 2. Radio Frame Structure.
</div>
This MIMO system uses a standard 3GPP LTE radio frame structure as shown in Figure \ref{fig:RF}. Radio frames of 10 ms duration are sub-divided into 10 subframes of 1 ms duration each. Each subframe contains two slots of 0.5 ms duration. A slot is further split into 7 OFDM symbols.

###  Resource Block

<div align=center>
  <img src="https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/imag/Resource%20Block.jpg" width="80%" />
</div>
<div align=center>
Fig. 3. Physical Resource Block Illustration.
</div>
This OFDM system utilize a total of 1200 subcarriers with the bandwidth 18MHz, of which are divided into 100 resource blocks (RBs), i.e., each RB contains 12 OFDM subcarriers, and the bandwidth of each subcarrier is 15KHz.

### OFDM Symbols Description
Each OFDM symbol carries a single signal type as listed below:
* Primary Synchronization Signal (PSS):The PSS is compliant with the LTE standard . The PSS sequence generation is implemented statically for Cell-ID 0.
* Pilot Signals: The same length-1200 quadrature phase-shift keying (QPSK) sequence is used to derive uplink and downlink pilots. Pilot sequences corresponding to different mobile stations are transmitted in a frequency orthogonal fashion, e.g., a pilot corresponding to mobile station 1 occupies the first subcarrier in each RB. A pilot corresponding to mobile station 2 occupies the second subcarrier in each RB and so forth. Note that in our 4*4 MIMO-OFDM prototyping system, users occupy 4 subcarriers of total 12 subcarriers in each RB. To estimated the MIMO channel, a radio frame must contain at least one uplink pilot symbol. A new MIMO channel estimate is obtained whenever a pilot symbol is received. The data symbol which follows this pilot symbol is equalized using this new channel estimate already. The channel estimate is held constant until the next pilot symbol is received.
* Physical Downlink Shared Channel (PDSCH): Downlink payload data is transmitted over the PDSCH without forward error correction coding. PDSCH processing comprises:
  * Scrambling using a polynomial in accordance to the LTE specifications.
  * Modulation in accordance to the LTE specifications. 
* Physical Uplink Shared Channel (PUSCH): The PUSCH is symmetric to the PDSCH.
* Guard: One OFDM symbol including cyclic prefix (CP) where nothing is transmitted in uplink or downlink direction.
Finally, we summarize the system main parameters as follows:

| **Parameter**     | **Value**    | 
| :-------------: | :-------------: |
| Center Frequency [GHz]      | 3.5     | 
|  Channel bandwidth [MHz]     | 20      | 
| Fast Fourier transform (FT) Size      | 2048      | 
| Number of used subcarriers     | 1200    | 
|  Number of RBs    | 100   | 
|  OFDM symbol duration [us]     |66.67     | 
| OFDM symbols per slot    | 7     | 
| Slot duration [ms]    | 0.5   |

## MIMO Channel Measurements
In the OTA test, we conduct two scenarios of indoor channel measurements, indoor-office, and indoor-hall. Each scenario including the static and dynamic MIMO channels.

<div align=center>
  <img src="https://github.com/www09324063/4x4-MIMO-prototype-system/blob/main/imag/scenario.jpg" width="80%" />
</div>
<div align=center>
Fig. 4. Illustration of two different measurement: the sky blue edges indicate the door and windows.
</div>

### Indoor-office measurements
The indoor-office measurements are conducted at a typical office room, where a wealth of scatterers and reflectors exists. 
As shown in (a), the base station is fixed in the central of the office room to collect uplink channel data, and four mobile antennas are separated into two different places.
The first case is a line-of-sight (LOS) case (marked in blue), where users are positioned close to the base station with LOS paths
available. The second case is non-line-of-sight (NLOS)case, where mobile antennas are surrounding the library with the
LOS path blocked by desks and tables (marked in pink red).
The sky blue edges indicate glass doors and windows.
We altered two setup configurations for the indoor-office measurements, including mobile antennas stay still and keep moving at a uniform speed of $1m/s$ inner the office room (horizontal plane only).

### Indoor-hall measurements
For the indoor-hall measurements shown in (b), we also selected the base station as receiver which fixed in the left central of a open indoor-hall.
Four mobile antennas remain stationary or slow-moving at a uniform speed of $1m/s$ in the front semicircle of the base station, which have LOS paths available to the base station.

## MIMO Channel Database
MIMO Channel Database can be download from GoogleDrive [here](https://drive.google.com/file/d/1-eUTTWh8ZjWfEVatLC91Mi_Zp9zIGL76/view?usp=sharing).

## AI Based Learning
### 1.群体智能算法
Git链接:(https://scikit-opt.github.io/scikit-opt/#/zh/README)
### 1.外部大模型学习资源链接
大模型基本概念和原理
- - - - - - - - - - - -  前置学习  - - - - - - - - - - - -
机器学习(Machine Learning,ML)
1 [机器学习](https://www.showmeai.tech/article-detail/185)
2 [吴恩达机器学习课程](https://www.bilibili.com/video/BV164411b7dx/?from=search&seid=5856176897296408924)
深度学习(Deep Learning,DL)
1 [神经网络](https://www.elastic.co/cn/what-is/neural-network)
[深度学习简介](李宏毅机器学习2022)
- - - - - - - - - - - -  LLM基础  - - - - - - - - - - - -
AI技术词扫盲
1 [人工智能](https://zh.wikipedia.org/wiki/人工智能)
[AGI](https://zh.wikipedia.org/wiki/通用人工智慧)
[AIGC](https://zh.wikipedia.org/wiki/生成式人工智慧)
[Large language model](https://zh.wikipedia.org/wiki/大型语言模型)
[NLP](https://zh.wikipedia.org/zh-hans/NLP)
2 [Prompt engineering](https://zh.wikipedia.org/wiki/生成式人工智慧)
[过拟合、欠拟合](https://www.hrwhisper.me/machine-learning-regularization/)
3 [fine-tuning](https://platform.openai.com/docs/guides/fine-tuning/fine-tuning)
[In Context Learning, ICL](https://www.hopsworks.ai/dictionary/in-context-learning-icl)
[Chain-of-Thought, CoT](https://www.promptingguide.ai/techniques/cot)
4 [RLHF](https://zh.wikipedia.org/wiki/基于人类反馈的强化学习)
大模型简介和技术发展趋势
1 [机器学习、深度学习发展历史]
2 [生成式AI](大模型发展史；常见大模型介绍；ChatGPT原理；Transformer原理)
3 [大语言模型简介](手把手教你炼大模型)
人工智能与大模型基础
1 [人工智能基础](李宏毅-机器学习课程)
2 [大模型科普&电信领域实践赋能系列课程]()
3 [大模型之美](大模型实战)
- - - - - - - - - - - -  LLM提示词  - - - - - - - - - - - -
prompt
1 [learnprompting](https://learnprompting.org/zh-Hans/docs/intro)
[提示工程指南](https://www.youtube.com/watch?v=yhk9x__D-Us)
2 [如何写好prompt]()
[prompt货架]()
[ChatGPT 中文调教指南](https://github.com/PlexPt/awesome-chatgpt-prompts-zh)
[prompt examples](https://platform.openai.com/docs/examples)
3 [openai prompt engneering](https://platform.openai.com/docs/guides/prompt-engineering/prompt-engineering)
4 [吴恩达教你写提示词](https://www.youtube.com/watch?v=gCbHoXL2IcA&list=PL1bD7CLmGebf9FewSIJGZhFDK6FyWBH7P)
- - - - - - - - - - - -  算法原理  - - - - - - - - - - - -
机器学习算法
1 [机器学习算法原理](李宏毅-机器学习课程)
[KNN](https://www.showmeai.tech/article-detail/187)
[逻辑回归](https://www.showmeai.tech/article-detail/188)
[朴素贝叶斯](https://www.showmeai.tech/article-detail/189)
[决策树](https://www.showmeai.tech/article-detail/190)
2 [随机森林](https://www.showmeai.tech/article-detail/191)
[回归树](https://www.showmeai.tech/article-detail/192)
[支持向量机](https://www.showmeai.tech/article-detail/196)
[聚类算法](https://www.showmeai.tech/article-detail/197)
[PCA降维](https://www.showmeai.tech/article-detail/198)
3 [GBDT](https://www.showmeai.tech/article-detail/193)
[LightGBM](https://www.showmeai.tech/article-detail/195)
[XGBoost](https://www.showmeai.tech/article-detail/194)
深度学习算法
1 [算法发展历史]
[深度学习简介]()
2 [梯度下降](https://www.showmeai.tech/article-detail/217)
[损失函数](https://www.showmeai.tech/article-detail/262)
[反向传播](https://www.showmeai.tech/article-detail/234)
3 [Transformers自注意力](https://www.showmeai.tech/article-detail/251)
[Transformer]()
4 [迁移学习算法]()
[联邦学习]()
[《深度学习》中的线性代数基础](https://www.jiqizhixin.com/articles/boost-data-science-skills-learn-linear-algebra)
5 [超参优化]()
——————————————————————————————————————————————————————————————————————————
模型架构
- - - - - - - - - - - -  小模型架构  - - - - - - - - - - - -
小模型架构
1 [多层感知机(Multilayer Perceptron, MLP)](https://www.zhuanzhi.ai/paper/e5998092a5230ac12f4ee9e134e57020)
2 [Long Short-Term Memory, LSTM](https://arxiv.org/pdf/1506.04214.pdf)
[LeNet](https://www.jiqizhixin.com/graph/technologies/6c9baf12-1a32-4c53-8217-8c9f69bd011b)
[AlexNet](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks)
[VGGNet](https://arxiv.org/pdf/1409.1556.pdf)
[Conditional GAN, CGAN](https://arxiv.org/abs/1411.1784)
[Deep Convolutional GAN, DCGAN](https://arxiv.org/abs/1511.06434)
- - - - - - - - - - - -  大模型架构  - - - - - - - - - - - -
大型卷积神经网络(Large Convolutional Neural Networks)
1 [ResNet](https://dragonbra.github.io/2022-03-06-ResNet-Notes/)
[Inception](https://arxiv.org/pdf/1409.4842v1)
[EfficientNet](https://arxiv.org/pdf/1905.11946)
大型循环神经网络(Large Recurrent Neural Networks)
1 [深层 LSTM(Deep LSTM)](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
[深层 GRU(Deep GRU)](https://arxiv.org/pdf/1406.1078.pdf)
Transformers
1 [Transformer]()
[BERT(Bidirectional Encoder Representations from Transformers)](https://arxiv.org/abs/1810.04805)
[GPT(Generative Pre-trained Transformer)](https://blog.csdn.net/shizheng_Li/article/details/123683218)
[T5(Text-to-Text Transfer Transformer)](https://arxiv.org/abs/1910.10683)
[BART(Bidirectional and Auto-Regressive Transformers)](https://arxiv.org/abs/1910.13461)
2 [GPT Models](https://platform.openai.com/docs/models)
3 [multi head机制](https://www.youtube.com/watch?v=hjesn5pCEYc)
大型生成对抗网络(Large Generative Adversarial Networks)
1 [StyleGAN](https://arxiv.org/abs/1812.04948)
[BigGAN](https://arxiv.org/pdf/1809.11096.pdf)
自监督学习模型(Self-Supervised Learning Models)
1 [SimCLR](https://arxiv.org/pdf/2002.05709.pdf)
[MoCo](https://arxiv.org/abs/1911.05722)
[BYOL(Bootstrap Your Own Latent)](https://arxiv.org/abs/2006.07733)
多模态模型(Multimodal Models)
1 [中文多模态数据集「悟空」](https://wukong-dataset.github.io/wukong-dataset/)
2 [中文图文表征预训练模型Chinese-CLIP](https://github.com/OFA-Sys/Chinese-CLIP)
——————————————————————————————————————————————————————————————————————————
大模型高阶应用
- - - - - - - - - - - -  RAG  - - - - - - - - - - - -
embedding
1 [embeddings](https://platform.openai.com/docs/guides/embeddings/what-are-embeddings)
2 [openai embedding uc](https://platform.openai.com/docs/guides/embeddings/use-cases)
3 [openai embedding model](https://platform.openai.com/docs/guides/embeddings/embedding-models)
向量数据库
1 [向量数据库有哪些](https://cloud.tencent.com/developer/article/2328915)
2 [向量数据库基本原理](https://guangzhengli.com/blog/zh/vector-database/)
3 [基于向量数据库的大模型增强]()
RAG
2 [RAG工程:使用领域专业知识]()
- - - - - - - - - - - -  langchain  - - - - - - - - - - - -
langchain
1 [LangChain](https://python.langchain.com/v0.2/docs/introduction/)
2 [langChain实战]()
- - - - - - - - - - - -  Agent智能体  - - - - - - - - - - - -
Agent智能体
1 [什么是智能体](https://www.53ai.com/news/qianyanjishu/2024052823549.html)
2 [智能体应用]()
3 [多智能体]()
[AI Agent未来发展研究方向 ]()
- - - - - - - - - - - -  常用工具  - - - - - - - - - - - -
常见工具
1 [AI辅助研发基础课]()
2 [AI工具集](https://ai-bot.cn/)
3 [ChatGPT技术分析]()
4 [AI辅助编码实战]()
——————————————————————————————————————————————————————————————————————————
大模型实战 
- - - - - - - - - - - -  开发框架  - - - - - - - - - - - -
开发框架
1 [pytorch](https://pytorch.org/tutorials/)
[tensorflow](https://www.tensorflow.org/tutorials?hl=zh-cn)
[scikit-learn](https://scikit-learn.org.cn/lists/2.html)
3 [搭建网络推荐系统](https://www.showmeai.tech/tutorials/43)
[应用搭建]()
- - - - - - - - - - - -  部署模型  - - - - - - - - - - - -
1 [Hugging Face](https://huggingface.co/docs)
3 [AI绘画](https://www.showmeai.tech/tutorials/43?articleId=312)
个人PC部署大模型
1 [ollama介绍](https://blog.csdn.net/fuhanghang/article/details/136677566)
2 [个人PC本地安装llamma、qwen、gemma大模型]()
- - - - - - - - - - - -  应用开发  - - - - - - - - - - - -
应用开发
[AI产品化开发]
### 2. 大模型学习路径
作者：数据慢慢跑
链接：https://www.zhihu.com/question/1959282826319995791/answer/1986477233553036839


