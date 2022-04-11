# KATE GPT3

This repository contains source code to our paper: 

* [What Makes Good In-context Examples for GPT3?](https://arxiv.org/pdf/2101.06804)
---

## 1. Introduction
Fine-tuning GPT3 requires hundreds of GPUs to load the 175B model, which is prohibitively expensive and time-consuming for ordinary research labs. Moreover, storing large fine-tuned model checkpoints require huge storage space.
To tackle these challenges, we propose **KATE** (**K**nn-**A**ugmented in-con**T**ext **E**xample selection), a non-parametric selection approach that retrieves in-context examples according to their semantic similarity to the test samples.
On several natural language understanding and generation tasks, the proposed method improves GPT-3’s performance, over the random sampling baseline, by a significant margin.

## 2. Inference Demonstration
To reproduce our TriviaQA result in the paper, please perform the following steps:
a. Download and unzip [demo_GPT3_KATE_TriviaQA_data.zip](https://drive.google.com/file/d/1ZbT97s72MilfldHZJHgL_TJ0yE6woK4_/view?usp=sharing). 
b. Move the unzipped files "trivia_qa_train_78785_dev_full_dev.tsv" and "trivia_qa_train_78785_dev_full_train.tsv" under the code directory "./inference/dataset/"
c. Move the unzipped files "trivia_qa_train_78785_dev_full_random_0.dat" and "trivia_qa_train_78785_dev_full_roberta-large-nli-stsb-mean-tokens_cosine_mean.dat" under the code directory "./inference/kNN_pretraining/".
d. To do inference on the TriviaQA dataset, please run the following commands:
```
export GPT3_KEY=*** # replace *** with your GPT3 API key
cd inference
chmod 755 run.sh
./run.sh
```

## 3. kNN Retrieval Demonstration
As shown in the above inference demonstration, the key step to do inference is to have the retrieved examples ready. We have computed and stored the indices of the training examples in a ".dat" file.
To reproduce the "trivia_qa_train_78785_dev_full_roberta-large-nli-stsb-mean-tokens_cosine_mean.dat" file above, please run the following commands:
```
cd inference
chmod 755 trivia_qa.sh
./trivia_qa.sh
```

In order to run the retrieval code, you need to install [Sentence-BERT](https://www.sbert.net/) in your environment in addition to all the packages listed in [requirements.txt](./requirements.txt).

### 3.1 Which Pre-trained Sentence Encoder?
In the paper, we study three sentence encoders for retrieval:

a. For the kNN_{roberta} results, you can import the pre-trained model RoBERTA-large from HuggingFace directly.
b. For the kNN_{nli} results, you can use the SentTransformer model called "roberta-large-nli".
c. For the kNN_{nli+stsb} results, you can use the SentTransformer model called "roberta-large-stsb".

<!-- ## Citing Our Work ##
If you find our work useful in your research, please consider citing the following paper:

```
} -->