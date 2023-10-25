# AI小冶—基于oneAPI的钢铁领域智能问答系统



### 团队名称：Devs

### 问题陈述：

##### （1）钢铁领域知识的复杂性

  钢铁工业拥有庞大而复杂的知识体系，涵盖了钢材的生产、加工、质量控制以及相关的设备维护、市场行情等方面。钢铁生产过程中包含多个工艺环节，如炼钢、连铸、轧制等，每个环节都有大量的技术知识和专业术语。此外，钢铁领域的材料特性、机械性能、质量标准等也需要钢铁工作者具备相应的知识。因此，快速高效地建立一个全面且准确的钢铁领域问答系统对于满足钢铁工作者的需求非常关键。

##### （2）传统信息获取方式的局限性

  目前，钢铁工作者通常依赖于手册、专家咨询和互联网搜索等方式来获取领域知识。然而，这些方式存在一些局限性。首先，通过手册查询的方式需要翻阅大量文献，耗时且容易遗漏信息。其次，专家咨询往往需要等待和预约，并且受制于专家的时间和资源限制。最后，互联网搜索虽然提供大量的信息，但存在信息质量参差不齐、缺乏钢铁领域专业性等问题。

##### （3）技术挑战

  钢铁领域问答系统的构建面临许多技术挑战。首先，钢铁领域的知识庞杂且复杂，如何建立一个全面而有效的知识库是一个重要问题。其次，钢铁工作者的问题通常涉及多个领域和专业术语，如何理解和解析这些问题提出了挑战。此外，如何从海量的数据中准确地获取和提取钢铁领域的知识也是一个关键问题。

### 项目简介：

   在当今信息时代，钢铁工业作为支撑现代工业的基础产业之一，扮演着重要的角色。然而，由于钢铁领域的复杂性和广泛性，钢铁工作者在日常工作中经常面临各种问题，需要快速、准确的获取领域知识和解决方案。传统的信息获取方式存在信息不全、响应时间长等问题，为了提高钢铁工作者的工作效率和准确性，开发一个智能、高效的钢铁领域问答系统具有重要意义。AI小冶系统旨在基于oneAPI工具构建一个钢铁领域的问答系统，通过构造钢铁领域问答数据集并在T5模型上使用oneAPI工具进行训练和微调。实验结果表明，我们成功实现了钢铁领域问题的准确回答，提高了训练和推理的效率，并展示出了系统的专业性和可行性。

### 技术栈及实现方案

#### （一）数据集构建

  为了构建AI小冶钢铁领域问答系统，我们首先采用了两个阶段的数据集构建过程。首先在第一阶段，我们构造了一个通用问答数据集，用于预训练中文T5模型。然后在第二阶段，我们构建了钢铁领域的专业数据集，用于在预训练模型上进行微调。

##### （1）第一阶段：通用问答数据集构建

  在第一阶段，我们构建一个通用的问答数据集，用于中文T5模型的预训练。我们从多个来源获取了大量的中文问答数据，包括开放问答社区、问答网站和公开的问答数据集。为了保持数据的多样性和广泛性，我们选择了涵盖各个领域、主题和难度等级的问题和对应的答案。
  通过数据清洗和预处理，我们去除了重复问题和低质量的数据样本，并进行了问题分析和分类。为了保证数据集的质量，我们还邀请了一些领域专家对数据进行验证和审核，确保问题和答案的准确性和可靠性。
  最终，我们构建了一个包含数百万个问题和答案对的通用问答数据集。该数据集涵盖了各种类型的问题，包括事实性问题、推理问题和主观性问题等。这个通用问答数据集将作为中文T5模型的预训练数据，提供丰富的语言知识和上下文理解能力。

##### （2）第二阶段：钢铁领域数据集构建

  在第二阶段，我们针对钢铁领域构建了专业的问答数据集，用于在预训练的中文T5模型上进行微调。我们的目标是让模型具备对钢铁相关问题的准确解答和领域专业知识的理解。
  为了构建钢铁领域数据集，我们采取了综合的数据收集策略。我们从提供的数据集以及钢铁行业的权威资料、专业书籍和行业标准中获取了大量的领域知识和问题样本。
    通过数据的清洗和整理，我们排除了重复和低质量的数据，保留了与钢铁领域相关的问题和对应的准确答案。我们对问题进行了分类和归纳，以便后续的模型训练和评估。
  最终，我们构建了一个钢铁领域问题和答案对的专业数据集。这个数据集涵盖了钢铁生产、工艺、设备、质量控制、市场行情等各个方面的问题。其中还包括了钢铁领域的术语、技术要点和实践经验等相关信息。
  通过构建这两个阶段的数据集，我们为钢铁领域的问答系统构建提供了丰富、准确且具有多样性的数据基础。第一阶段的通用问答数据集为中文T5模型的预训练提供了丰富的语言知识和背景理解能力，而第二阶段的钢铁领域数据集为模型的微调和专业化提供了具体领域的问题和答案样本。

#### （二）模型设计

  为了构建AI小冶钢铁领域问答系统，我们采用了T5模型作为基础模型，并分两个阶段对其进行了训练。第一阶段通过通用问答数据集的预训练提供了模型的语言理解和生成能力，第二阶段通过钢铁领域数据集的微调使模型具备钢铁领域问题的解答能力和专业知识。

![image]([\fig\11.png](https://github.com/Achilles008/oneapi_AIxiaoye/blob/main/fig/11.png))

##### （1）模型预训练

  在第一阶段，我们使用大规模的通用问答数据集对T5模型进行预训练。中文T5模型是一个基于Transformer架构的多任务学习模型，具备了生成型和理解型任务的能力。
  预训练的目标是让模型通过自监督学习的方式学习到广泛的语言知识和上下文理解能力。我们将通用问答数据集输入模型中，将问题和答案作为输入序列，并通过预测缺失的答案或生成问题的方式进行训练。我们采用了掩码语言模型（Masked Language Model，MLM）等技术来训练模型。
  预训练过程中，我们设置了合适的超参数，如学习率、批量大小和训练步数等，以优化模型的预训练效果。同时，我们通过Intel® Extension for PyTorch工具实现模型的分布式训练，并加速反向传播的效率，大大节省了训练时间。通过大规模的预训练数据和适当的训练策略，我们使得中文T5模型能够学习到丰富的语言模式和表征能力。

##### （2）钢铁领域数据微调

  在第二阶段，我们使用钢铁领域的专业数据集对预训练的中文T5模型进行微调，以提高模型在钢铁领域问题回答的准确性和专业性。
  微调的过程可以看作是有监督学习任务，我们将钢铁领域的问题和答案对作为训练样本。我们将微调数据集划分为训练集、验证集和测试集，并使用训练集对模型进行训练，使用验证集对模型进行调优，最后通过测试集对模型的性能进行评估。
  微调过程中，我们调整了微调的超参数，如学习率、批量大小和微调步数等，以使模型在钢铁领域的问题回答上获得更好的性能。我们使用最大似然损失函数来度量模型的预测和真实答案之间的差异，并通过反向传播算法进行参数优化。

![](\fig\22.png)

#### （三）Intel® Extension for PyTorch工具的使用

##### （1）分布式训练和性能优化

  我们队基于Intel® Extension for PyTorch 对分布式训练的支持，使得我们可以在多个GPU设备上进行协同训练，加快训练速度和提高效率。同时，它还利用 Intel® 数据并行合并技术，将多个小批量数据合并成一个大批量数据进行并行计算，以提高训练性能。

##### （2）优化正向传播和反向传播

  Intel® Extension for PyTorch 利用 Intel® Math Kernel Library (Intel® MKL) 和 Intel® Deep Neural Network Library (Intel® DNNL) 等优化库，加速正向传播和反向传播的计算。这些优化库使用了针对 Intel® 架构的高性能数学和深度学习函数实现，从而提高我们模型训练的速度和效率。

##### （3）模型加速和自动混合精度

   Intel® Extension for PyTorch 提供了针对模型加速的功能，针对卷积和矩阵运算的 AVX-512 向量神经网络指令 (AVX512 VNNI) 和 Intel® Advanced Matrix Extensions (Intel® AMX) 等指令，以及自动混合精度功能，将浮点数计算转换为低精度计算，提高我们模型的计算速度和效率。

#### （四）Intel® Neural Compressor工具的使用

##### （1）模型压缩和量化

  我们队使用了 Intel® Neural Compressor 的模型压缩和量化功能，通过减少模型的参数数量和模型的表示精度，从而降低模型的大小和计算复杂度。我们使用低比特量化技术，将模型中的浮点参数转化为低比特整数表示，从而大幅度减少模型的存储空间和计算开销。

##### （2）自动化模型优化

  我们队也使用了 Intel® Neural Compressor 提供了自动化模型优化功能，通过分析模型的结构和权重分布，自动推断最佳的压缩策略和参数设置。这样可以减少我们的手动调整和优化工作，提高模型优化的效率和一致性。

##### （3）硬件加速支持

  Intel® Neural Compressor 支持在特定硬件平台上进行模型推理的加速。在未来，我们队将会使用 Intel® DL Boost 技术，利用硬件指令集和特定硬件加速器，如 Intel® Xeon® 处理器上的 Intel® AVX-512 VNNI 指令集，加速模型的计算过程，从而提高模型的推理性能和效率。

### 团队学到了什么：

  我们团队学到了许多oneAPI使用相关的知识和经验:

##### （1）平台无关性

  oneAPI提供了一种开放的标准，使得我们的项目能够轻松迁移到多种硬件平台上，如CPU、GPU和FPGA等。我们学到了如何利用oneAPI的平台无关性，优化和扩展我们的方案，提高项目的可移植性和适应性。

##### （2）高性能计算

   oneAPI提供了高性能计算的能力，可以利用硬件加速器和优化的算法，实现对大规模数据的快速处理和分析。我们学到了如何选择合适的硬件平台，如何优化算法和如何进行并行处理，以实现高效和准确的数据处理和分析。

##### （3）开放生态系统

  oneAPI的生态系统由多个开源工具、库、框架和社区组成，为项目开发和优化提供了丰富的资源。我们学到了如何利用oneAPI工具和库，如英特尔® AI 分析工具套件，以及如何与社区进行交流和分享，加速项目的开发和改进。

  通过这些学习和应用，我们团队深入了解了oneAPI的优势和特点，提高了项目的技术水平和创新能力，为钢铁行业的智能化转型和发展做出了贡献。

### 代码运行

#### 安装库(Python 3.8.5 | CUDA 10.2)

```
contractions==0.0.52
ftfy==5.9
inflect==5.3.0
nltk==3.5
numpy==1.19.2
scikit_learn==1.0.2
spacy==3.1.1
tensorboardX==2.5
torch==1.8.0
tqdm==4.62.3
transformers==4.11.3
vaderSentiment==3.3.2
```

#### 运行命令

```
python train.py   #模型训练
python quantize.py  #模型量化
python inference.py   #模型推理
```

#### 注意事项

​    由于目前科研原因，预训练与微调的数据集暂时无法开源

### 致谢

​    感谢以下开源项目的启发：

https://github.com/Sahandfer/CEM/tree/master

https://github.com/oneapi-src/vertical-search-engine

https://github.com/oneapi-src/disease-prediction

https://github.com/Morizeyao/GPT2-Chinese

https://github.com/thu-coai/CDial-GPT

https://github.com/Shivanandroy/simpleT5

https://github.com/chenjunyi1999/ChatBot-GPT2

https://github.com/pemagrg1/text_summarization
