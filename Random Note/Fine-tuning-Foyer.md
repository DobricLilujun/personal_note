# Fine-Tuning Required Resource

## Fine-tuning Definition

Fine-tuning refers to the process of further training a pre-trained model on a specific task's dataset to adapt the model to that task. During fine-tuning, most of the pre-trained model's parameters are typically frozen, and only a small subset of parameters relevant to the specific task is updated to reduce the consumption of computational resources and time. Fine-tuning allows the model to exhibit improved performance and generalization on the specific task.

## Fine-tuning Methods

Language models such as Llama are more than 10 GB or even 100 GB in size. Fine-tuning such large models requires instances with significantly high CUDA memory. Furthermore, training these models can be very slow due to the size of the model. Therefore, for efficient fine-tuning, we use the following optimizations:

1. Low-Rank Adaptation（LoRA）：This is a type of parameter efficient fine-tuning (PEFT) for efficient fine-tuning of large models. In this, we freeze the whole model and only add a small set of adjustable parameters or layers into the model. For instance, instead of training all 7 billion parameters for Llama 2 7B, we can fine-tune less than 1% of the parameters. This helps in significant reduction of the memory requirement because we only need to store gradients, optimizer states, and other training-related information for only 1% of the parameters. Furthermore, this helps in reduction of training time as well as the cost. 
2. **Int8 quantization** – Even with optimizations such as LoRA, models such as Llama 70B are still too big to train. To decrease the memory footprint during training, we can use Int8 quantization during training. Quantization typically reduces the precision of the floating point data types. Although this decreases the memory required to store model weights, it degrades the performance due to loss of information. Int8 quantization uses only a quarter precision but doesn’t incur degradation of performance because it doesn’t simply drop the bits. It rounds the data from one type to the another. 
3. **Fully Sharded Data Parallel (FSDP)** – This is a type of data-parallel training algorithm that shards the model’s parameters across data parallel workers and can optionally offload part of the training computation to the CPUs. Although the parameters are sharded across different GPUs, computation of each microbatch is local to the GPU worker. It shards parameters more uniformly and achieves optimized performance via communication and computation overlapping during training.

## Fine-tuning with LlaMA2

Below are some relevant papers that describe the resources used and the final results achieved in fine-tuning LlaMA2.

| Article Name                                                 | Fine-tuning Description                                      | Fine-tuning result                                           | Required Resource                                            |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| LLaMA-Adapter: Efficient Fine-tuning of Language Models with Zero-init Attention | Introducing a lightweight adaptation method called LLaMA-Adapter, which efficiently transforms the LLaMA model into a high-performing instruction-following model by introducing only 1.2 million learnable parameters on the frozen LLaMA 7B model. | The efficiency of LLaMA-Adapter enables it to perform large-scale language model fine-tuning on mobile devices. | The training time on 8 A100 GPUs is less than one hour.      |
| Financial News Analytics Using Fine-Tuned Llama 2 GPT Model  | For inputting millions of documents into LLM, a full fine-tuning approach can be used. However, in cases of smaller datasets, the PEFT/LoRA method can be employed, which fine-tunes only a small subset of model parameters. This method is used for analyzing text from a financial market perspective, highlighting key points in the text, summarizing the text, and extracting named entities with appropriate sentiment. PEFT/LoRA. | The fine-tuned Llama 2 model can perform multi-task financial news analysis according to a specified response structure, with a portion of the response being structured text. | Google Colab.                                                |
| ChatDoctor: A Medical Chat Model Fine-Tuned on a Large Language Model Meta-AI (LLaMA) Using Medical Domain Knowledge | Fine-tuning with Lora PEFT/LoRA                              | Through extensive experiments, researchers have found that models fine-tuned on patient-doctor dialogues outperform ChatGPT models in terms of metrics like precision, recall, and F1 score. | Google Colab.                                                |
| RadOnc-GPT: A Large Language Model for Radiation Oncology    | Fine-tuning with Lora PEFT/LoRA                              | Compared to general large language models, the evaluation results, based on comparing the output of RadOnc-GPT, demonstrate a significant improvement in clarity, specificity, and clinical relevance in the output generated by RadOnc-GPT. | Google Colab.                                                |
| **QLoRA: Efficient Finetuning of Quantized LLMs**            | **Fine-tuning with QLoRA**                                   | **QLoRA propagates gradients back to low-rank adapters (LoRA) from a frozen 4-bit quantized pre-trained language model. Our best model series, which we named "Guanaco," outperforms all previously publicly released models in the Vicuna benchmark, achieving a performance level of 99.3% compared to ChatGPT.** | Fine-tuning a 65-billion-parameter model on a single 48GB GPU while preserving the full 16-bit fine-tuning task performance. |

One of the most noteworthy aspects is LoRA and QLoRA, which can significantly reduce the resources required for training. According to some estimates, if we use 32-bit precision to represent floating-point numbers, a model with a hundred parameters would require 100 x 4 x 5 = 2,000 bytes of memory. Scaling up, a model with a billion parameters would need 1e9 x 4 x 5 = 2e10 bytes, which is equivalent to 20 gigabytes (GB) of memory for every billion parameters. However, with various optimization strategies, the computational resources required for fine-tuning can be reduced to the scale of a few GPUs. The following image illustrates the specifications of the instances required by Amazon for training Llama 2.

![1111](https://raw.githubusercontent.com/DobricLilujun/imagesAll/main/images1111.PNG)

Llama 2 70B, under three optimization strategies, still requires a minimum of 192GB of memory for fine-tuning. In contrast, QLoRa can fine-tune a 65-billion-parameter LlaMa model on a single 48GB GPU while maintaining the full 16-bit model performance. The specific comparison of different Amazon instances is as follows.

![Capture](https://raw.githubusercontent.com/DobricLilujun/imagesAll/main/imagesCapture.PNG)

## Conclusion

In fine-tuning the 70-billion-parameter Llama 2 model, under the conditions of applying full QLORA, FSDP, and Quantization, the estimated resource requirements are approximately 48 gigabytes (48G), and the fine-tuning time is expected to be less than a day. The specific training time depends on factors such as the dataset size, the fine-tuning approach, and the performance of the GPU.。



## Fine-tuning weekly meeting 2023-10-24

Main topic:

1. Document Classification
2. Entity Recognition of Information Extraction
3. Document Summarization and Evaluation
4. Interactive User Queries and interaction with PDF files (Txyz.ai)



Topic of meeting

1. Ollama is a user friendly llm tool using that we can interact with llm directly; But not in the fine-tuning field.

   1. By running 

      ```
      ollama run llama2
      ```

      Ollama can directly download llama2 model, deploy it and open a terminal interactive interface to let you chat with LLMs.

   2. Importing models by  GGUF models in the Modelfile

   ollama advantages: https://noted.lol/ollama/

   neo4j+ ollama + langchain tutorial: https://collabnix.com/getting-started-with-genai-stack-powered-with-docker-langchain-neo4j-and-ollama/

   

2. Lacking of resource for running the model (Can only access by HPC but difficult to build environment - Need time)

   | Model              | Parameters | Size  | Download                       |
   | ------------------ | ---------- | ----- | ------------------------------ |
   | Mistral            | 7B         | 4.1GB | `ollama run mistral`           |
   | Llama 2            | 7B         | 3.8GB | `ollama run llama2`            |
   | Code Llama         | 7B         | 3.8GB | `ollama run codellama`         |
   | Llama 2 Uncensored | 7B         | 3.8GB | `ollama run llama2-uncensored` |
   | Llama 2 13B        | 13B        | 7.3GB | `ollama run llama2:13b`        |
   | Llama 2 70B        | 70B        | 39GB  | `ollama run llama2:70b`        |
   | Orca Mini          | 3B         | 1.9GB | `ollama run orca-mini`         |
   | Vicuna             | 7B         | 3.8GB | `ollama run vicuna`            |

3. QLORA: Efficient Finetuning of Quantized LLMs

   Much more efficient and still have other method to save memory

   Need to explore





1. Fine-tuning llama2 using public dataset

2. Search similar contributions of the same STOA

3. Named entity resolution in public dataset

   

