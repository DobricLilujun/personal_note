# 2023-11-05 - Weekly Meeting





## Docker

Docker is a virtual environment image container





```
Already set up docker to install docker

apt-cache madison docker-ce // Trying to make sure every version is okay



```



### Tutorial



Content:

**Basic tool of a system: apt-utils, wget etc**

**Python 3.11**

**Anaconda**

**Pip** 

**A venv tool box**

**Creation of a environment called llm_env**

**CUDA 12.3**



docker run --runtime=nvidia -it docker.io/library/llm_env:1.1

nvidia-smi check cuda version

CUDA 11.8

Auto gptq has a severe version constraints



source /home/lujun/local/docker/.venv/bin/activate

pip freeze > requirements.txt

```
For CUDA 12.1: pip install auto-gptq
For CUDA 11.8: pip install auto-gptq --extra-index-url https://huggingface.github.io/autogptq-index/whl/cu118/
For RoCm 5.6.1: pip install auto-gptq --extra-index-url https://huggingface.github.io/autogptq-index/whl/rocm561/
For RoCm 5.7.1: pip install auto-gptq --extra-index-url https://huggingface.github.io/autogptq-index/whl/rocm571/
```

check cuda version :

ls -l /usr/local | grep cuda

or

cd /usr/local/

show the cuda version you isntalled



Build:

docker build --runtime=nvidia -t llm_env_cuda:1.3 . 

pip freeze > requirements.txt



docker build -t llm_env_cuda:1.6 .

docker run --runtime=nvidia -it llm_env_cuda:1.5





## Qlora with Mistral- Fine-tuning



Work really well avec un gpu de 24G sur google colab

Notebook 



## Research



1. **ChainForge** is a framework for batch testing prompts using a user interface and customizable evaluation, along with visualization of results. This framework could be utilized not only for testing the prompt engineering of LLM, but also for creating new datasets for training. It is **frequently updated**

   

2. **Gcastle** is a tool developed by Huawei that **integrates various causal inference methods** and we can use it as a toolbox. This could prove very useful in creating multiple new metrics, which can be employed in ChainForge to evaluate response quality.

   ​	size of the chunking analysis according to causality analysis

   ​	size of quantization influence on quality

   ​	

   

3. The main problem is to find different metric for evaluations:

   1. Evaluation of the results of Information extraction
   2. Evaluation of causal relation between A and B
   3. **Whether Causal relation in LLM is simple unexplorable filed because they only have  attention models?** 
      1. Idea of **ablation test** to test causal
      2. Lacking of metric  





Fine tuning  - Json

Avoir un dataset pour on puisse tester

Paperspace 

lamda lab



  --   Tarif, comment ca marche

  --   Marche pour toutes les equibpe 

  --   



### Objectif

1. Choix de platform



2. Parties fine-tuning - Different model fintunign sur mistral

   ​	langue du prompt 

   ​	quantisation

   ​	longeur de prompt

   3. changer a 10 a 11 every two weeks



Pipeline :

 	1. Chain forge : find params , which llm, emedding size, size of quantization (firstly gpu)
 	2. Genereal condition: what do we need to extract for the foyer
 	3. One of the model, test chain forge with one model
 	4. All the model and all embedding size to test (second week) find other descripiton on the quality of the output





# Summary of Weekly Meeting (2023-11-05)

## Docker

The meeting began with a discussion on Docker, focusing on creating a virtual environment image container. The tutorial covered essential tools for a system, including apt-utils and wget, as well as the installation of Python 3.11, Anaconda, Pip, and a venv toolbox. An environment named "llm_env" was created, incorporating CUDA 12.3. The use of the 'docker run' command with NVIDIA runtime was demonstrated to check the CUDA version. Auto-gptq was highlighted for CUDA version constraints, with specific installation instructions provided.

## Qlora with Mistral- Fine-tuning

The team reported successful usage of Qlora with Mistral for fine-tuning on Google Colab with a 24G GPU. Notebooks were specifically mentioned in this context.

## Research

### 1. ChainForge

ChainForge, a framework for batch testing prompts with customizable evaluation and result visualization, was introduced. It is frequently updated and can be employed for prompt engineering testing and creating new training datasets.

### 2. Gcastle

Gcastle, a Huawei-developed tool integrating various causal inference methods, was discussed as a useful toolbox. It can aid in creating new metrics for ChainForge evaluation, including chunking analysis based on causality analysis and quantization influence on quality.

### 3. Metric Evaluation Challenges

The team addressed the challenge of finding metrics for evaluation, including information extraction results and causal relations. Questions were raised about the simplicity of causal relations in LLM due to its attention models, leading to the proposal of an ablation test. The team expressed a need for additional metrics.

## Fine-tuning - Json

Discussion shifted to fine-tuning using JSON, emphasizing the importance of having a dataset for testing. Platforms such as Paperspace and Lamda Lab were mentioned.

## Objectives

1. **Platform Selection:** The team aims to decide on a platform for their work.
2. **Fine-tuning Variations:** Exploration of different model fine-tuning aspects on Mistral, including prompt language, quantization, and prompt length. Changes are planned every two weeks.
3. **Pipeline:** The proposed pipeline includes parameter discovery using ChainForge, identifying conditions for generalization, testing one model with ChainForge, and conducting comprehensive tests on all models and embedding sizes.
