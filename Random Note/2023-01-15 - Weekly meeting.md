# 2023-01-15 - Weekly meeting

1. Prompt     injection detection as a classification tasks
2. Prompt     prior evaluation method: Better prompt, Promptfoo 
   1. https://github.com/stjordanis/betterprompt
   2. https://github.com/promptfoo/promptfoo
3. Prompt     engineering with ChainForge, LangchainFlow, PromptFlow, ML flow
4. Causal     analysis of the parameters and build the pipline
   1. Find      10 documents of insurance or other domain
   2. Determine      one or several parameters as the simulation input
   3. Determine      the prompt that we need to use and the evaluation metrics for the quality      of the output

​                                i.   https://www.trulens.org/

​                               ii.   https://github.com/stanford-futuredata/ARES

​                              iii.   RAGAS: https://arxiv.org/abs/2309.15217   https://bajpaihimanshu.medium.com/papermadeeasy-ragas-automated-evaluation-of-retrieval-augmented-generation-ccfe5ea50db0

 

1. Do      the simulation and gather the data
2. Use      gcastle to build the causal inference graph and causal inference analysis
3. Generalize      the pipline and do more simulations



## Fine-tuning



Things achieved during the past two weeks:



**Concentration** on the dataset building for fine tuning of Mistral/and investigating Mistral.

-Successfully Fine Tuning testing for Mistral  on Paper space (testing before migrating to GPU).

-Investigated new tool: **Wandb** as a intermediate model result visualization in real time 

1. Different checkpoint can be saved on the disk to be loaded
2. The data has been uploaded on a website
3. Real-time training status loading

![Mistral-Fine-Tuning](https://raw.githubusercontent.com/DobricLilujun/imagesAll/main/imagesMistral-Fine-Tuning.PNG)

Preparing insurance training dataset from insuranceQA

​		https://github.com/shuzi/insuranceQA 

​		Very good dataset in the insurance industry 7 years ago and 

​		Corpus Statistics



|                                                              | Question | Answer | Question Running Words |
| ------------------------------------------------------------ | -------- | ------ | ---------------------- |
| Train                                                        | 12,889   | 21,325 | 107,889                |
| Valid                                                        | 2,000    | 3354   | 16,931                 |
| Test                                                         | 2,000    | 3308   | 16,815                 |
| There are totally 27,413 answers (answer set size is 27,413) with the 3,065,492 running words of answers. |          |        |                        |

https://github.com/white127/QA-deep-learning





**1. Avoid overfitting**

**2. knowledge distillation**

**3. Find a way to generate more question**

4. **Table GPT**

**5. An article table-to-text generation**







Two week planning:

1- extraction for data set

2-Qlora fine-tuning on general dataset.

3- Generate a new ground truth dataset [labeled and structured] for Foyer using gpt4

3-Re-Fine-tuning Mistral on the customized generated dataset.







## Excel For LLM model Params

Goals achieved: 

-Defining the parameters that should be tested/explored to check the causal inference on the LLM output.

Question: Priority of parameters ? Which parameters to choose? 

| Chunk Size - Fixed-size chunking                             |
| ------------------------------------------------------------ |
| Context Size                                                 |
| Quantization Size                                            |
| Model Structure                                              |
| Complexity of user queries                                   |
| Length of the user queries                                   |
| Sentence splitting  (NLTK, spaCy) Recursive Chunking Specialized Chunking |
| Range of Chunk Sizes                                         |
| Model Size                                                   |
| Document Or Context Type (Table, Graph Or Citation)          |
| Context Description Quality(Good or Bad)                     |
| Question position (Start, mid, end)                          |
| similarity search                                            |
| Temperature level                                            |
| Model loading precision (4 bits or 16 bits)                  |
| Context Fruitfulness (Large, middle, small)                  |
| Contex Relativeness To the question                          |
| Context key information Positions                            |
| Precision in Instruction (the “who, what, where, when, why, how” framework) |
| Uncertainty Evaluation and Retrieve  (Let them reconsider if they do not know the answer) |
| Step-by-Step Thinking COT Structure                          |
| Step-by-Step Thinking COT Chain length                       |
| Vector Data Related Params  (Annoy、Faiss by Meta、Milvus和Pinecone) |



## Hackthon



- Successfully won the hackathon organized by Foyer.
- The hacakthon took 2 days of continuous work.

Ideas developed were:

1. Document information retrieval using Langchain:

	1. Information are retrieved from the context at the very beginning 
	
	1. Automatic generation of questions by using LLMs, to be used by the chatbot that will ask the users for additional information.
	
	1. The model gets finally all the information needed and ends the conversation
	
	   

Some drawbacks: 

-Not very stable in terms of the coding level

-Some human made trap can mislead the model to have a wrong answer

-We think the prompt generated needs to be modified and optimized

But **We won!**





## HPC and Paperspace

1- Successfully ran the first model on the UL-HPC and working on running the developed Docker file on UHPC.

2- Building knowledge on Submit jobs, Interactive execute the notebook and use gpu, Submit directly notebook execution tasks



Problems faced: 

- Missing a clear and easy  pipeline for using the GPU on HPC

temporary solution:

1. I just bought the paperspace GPU for testing 





# Conference

The 38th Annual AAAI Conference on Artificial Intelligence

https://llmcp.cause-lab.net/submit-llmcp





# Causal Inference with LLM

https://www.youtube.com/watch?v=RbzAtlVopAU

1. Faster test for Graph discovery (KCIT ,RCIT)
2. Linear models with non-gaussian noise, or non-linear model(LinGAM)
3. Gradient based formulated as a continuous optimization problem and use deep learning.



Causal task:

	1. Effect estimation: How much a effects b
	1. Counter-factual: if A had a different value, what happens
	1. Attribution: why did B change
	1. Prediction:  What happen when A changed in the future.





STOA:

1. Casual analysis has been restricted to tabular data, leaving aside rich text or data
2. How to combine existing graph discovery algorithms with llms
   1. LLMs to reduce size of Markov equivalence graphs (for constraint-based algorithm)
   2. LLM as priors for score based algorithm
3. How to obtain a confidence score for causal relationships from LLM output?
4. Can LLMs enable end-to-end learning for downstream causal tasks like effect t estimation or attribution?



**How to let LLM to inference variables or causal graph efficiently?** **Causal Prompt**



https://github.com/py-why/pywhy-llm
