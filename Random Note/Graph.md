# Graph of Thought

## Question Modeling

Information extraction model (IE) is **the automated retrieval of specific information related to a selected topic from a body or bodies of text**. 

## Structure Comparison

GoT modeling in the paper

1. Choose the problem and define it
2. Human thinking about the specific step-by-step solution of the problem and articulate these steps into several phrases
3. LLMs generated different thoughts (results) within one step in a sub questions and aggerate the results in the next step. At the same time, the program (GoO) as the static structure scores different thoughts.
4. Step by step, the GoT obtain the final solutions.

![111](https://raw.githubusercontent.com/DobricLilujun/imagesAll/main/images111.PNG)

GoT Modeling 

1. Encountering a problem, based on **problems descriptions** and **online searched step-by-step solutions** ,create potential cause issues of the problems as a know graph (Heterogeneous information) (Brain storming of LLMs)

   Problem descriptions and online searching step-by-step solutions can be used to generate thought graph T1, T2, ... Tn

2. Construct weighted and directional graphical model 

3. Counterfactual analysis empowers in the graph to enhance model's logical capability

4. Scoring causality inference step by step

5. Find the best graph path and then generate the solution as GoT model in the paper

## Summary OF the Talk 2023-10-09

Information extraction (IE) & email extraction

Questions to be asked with Geoffrey:

- What is the knowledge graph in Foyer?

- what is the workflow of contract claim?  Understand the work flow

- Workflow of the contract IF

- Other user cases or problems need to be solved

- Long-term vision of Foyer Group

  

Tasks to do:

1. calassifer des document: sininstrem ==, famille de contract 

​		42% 85%  sinister premier etape au fil de l'eau

2. extraction des informaiton:
3. resumer des informaitons
4. poser le question.  txyz.ai

decrire les cas d'usage

- Get papers for **IF using llms** in the papers

- Finetuning **llama2 to IF** or trying other prompts (auto-prompt) lora 

  - Robin pas tester fine tuning

    

- Find an approach of **auto-prompts for llama2** trying to using public dataset, foyer. See the result

  - auto-gene 

  - langchain

  - auto prompt

    poc chatgpt: langchain llm

    

- Combining majority voting , + benchmarking  LLMs in IE be finished at mid of November (**Make a list of IF with LLM**)

  

- Workshop papers December. 

- Task making  tools to let users to use model for IE after the workshop papers

- Causality analysis  (instruct GPT and Graph of thought analysis)

  

```markdown
Chain of Prompt 
IF using llm papers finding it?
Knowledge graph how to access the data - 
Causality:
​	install llama2 finetuning llama2 fining tunign llama2 to extract news paper
​	What data set and model redo data set test llama 
idea:
​	 three models vote majority
​	 Small toolbox to develop extension tools to contract stream lit
idea:
​       Causality of putting certain node  link between path analysis causality
```







​	

​	
