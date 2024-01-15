# 2023-11-05 - Weekly Meeting

## Paper Searched

**A GPU tutorial**



**Tim Dettmers**: Which GPU to get for Deep Learning?

​	They have train 1000 models 

​	Quality is better than size

​	Lora parameter for deploying



1. LORA: Low rank adaptation of large language model

   Freeze weights and add trainable rank decomposition metrics in each layer of transformer structure

   <img src="https://raw.githubusercontent.com/DobricLilujun/imagesAll/main/images333.PNG" alt="333" style="zoom: 80%;" />

   Reduce trainable weights 10k times and reduce GPU memory required by 3 times

   **No additional inference latency**

   **Unclear of underlying mechanism**

   

2. QLORA: Efficient Finetuning of Quantized LLMs

   A significant fine-tuning shift from 780g to 48 g

   Benchmark: 

   ​	Fine-tuning Llama: Vicuna benchmarking 90% chatgpt 

   ​	Elo ratings: The winner of a match is determined by GPT4 , competetion between llm

   ​	ShareGPT: Data set sharing with online gpt

   ​	ChatBot Arena: 

   ​		Competition  https://arena.lmsys.org/

   ​		Leader board: https://arena.lmsys.org/

   ​	WebNLG:

   Methology:

   ​	4-bit Normal Float quantization:

   ​		Using 4-bit Float to save the weight instead of 16 float it self 

   ​		**12 bit reduction per weight**

   ​	Double quantization:

   ​		**0.5 bit / weight to 0.127bit/ weight  -> 0.373 bit reduction per weight**

   ​	Paged Optimizers:

   ​		Nvidia memory optimizer function; Unified memory using CPU RAM

   ![1234](https://raw.githubusercontent.com/DobricLilujun/imagesAll/main/images1234.PNG)

   Evaluation: 

   ​	Using human and ChatGPT4

   ​	**Using Lora for fine-tuning a small size model could perform better than using normal fine-tuning method to fine-tuning a larger size model**

   ​	Using only 0.2 % of the original model weights for fine-tuning

   Inconvenient:

   ​	**Math is really bad**; Need to be solved

   ​	Good in inference

   

## Progress

1. Build a knowledge sharing repository of Gitlab:
2. Building the environment based on HPC using singularity

1. Clean the documents

2. Classification of documents into sub-category and sub-sub category

3. Extraction of the information according to different categories

4. Finding a method to control the correctness and precision of these work as a baseline ground truth of human work

5. Chat with document to give precise information and reasoning process to users according to exactly the documents

6. **Qlora** could be a solution for low cost fine-tuning solutions

7. Training inside the local machine is not a constraint any more

   

## Mail Content

### Progress

The meeting covered several ongoing activities and progress updates:

1. Documents are being categorized into sub-categories and sub-subcategories, and Data Studio has already shown significant results, achieving an accuracy rate of approximately 80%-90% in both classification and information extraction.
2. We plan to explore various methods to ensure the correctness and precision of their work, serving as a baseline for human work, and potentially increasing the accuracy rate if possible. This may involve techniques like chunk size analysis and causal analysis of input and output.
3. We discussed that fine-tuning is no longer limited to local machines, as we now have remote access to the server.
4. A knowledge sharing repository on Gitlab is in development at https://gitlab.uni.lu/luli/foyerllm.git.
5. The team is actively working on creating a training environment based on HPC using Singularity, and a comprehensive tutorial will be prepared.
6. The team will also explore https://www.lasa.ai/, an open-source chatbot shared by Lama, which could potentially be integrated directly into Foyer.

### Papers

One of the content of the meeting is Qlora which largely decrease the GPU resource needed to fine-tuning the model:

- The researchers have trained 1000 models, emphasizing that quality is more important than size.
- We mentioned "LORA," an acronym for "Low rank adaptation of large language model," which involves freezing weights and adding trainable rank decomposition metrics in each layer of the transformer structure. This approach reduces trainable weights by 10,000 times and reduces GPU memory requirements by three times without introducing additional inference latency. However, the underlying mechanism remains unclear.
- The paper "QLORA: Efficient Finetuning of Quantized LLMs" was also discussed. It showcased a significant fine-tuning shift from 780g to 48g. The benchmarking and evaluation involved various methods, such as "Fine-tuning Llama: Vicuna benchmarking 90% ChatGPT," Elo ratings, ShareGPT data set sharing, ChatBot Arena competition, and WebNLG. The paper proposed methods like "4-bit Normal Float quantization" and "Double quantization" to reduce weight bit rates, with promising results. However, there were concerns about the mathematical aspects of the paper, which need further clarification.

