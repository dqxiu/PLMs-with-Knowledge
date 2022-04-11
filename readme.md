
# Paper Notes on Pretrain Language Models with Factual Knowledge


<!-- omit in toc -->
## Contents


- [Paper Notes on Pretrain Language Models with Factual Knowledge](#paper-notes-on-pretrain-language-models-with-factual-knowledge)
  - [Introduction](#introduction)
    - [Keywords Convention](#keywords-convention)
  - [Papers](#papers)
    - [Survey](#survey)
    - [Probing](#probing)
    - [Knowledge Retrieving](#knowledge-retrieving)
    - [Knowledge Injection](#knowledge-injection)
    - [Model Editing](#model-editing)
      - [Baseline](#baseline)
      - [Method](#method)
      - [Evaluation](#evaluation)
    - [Continual Pretraining](#continual-pretraining)
    - [Model Editing v.s. Continual Learning](#model-editing-vs-continual-learning)




## Introduction

This is a paper list about **PLMs & Knowledge**. 

### Keywords Convention

![](https://img.shields.io/badge/FaE-DCE7F1) abbreviation 

![](https://img.shields.io/badge/Efficient-EAD8D9) key features

![](https://img.shields.io/badge/QA-D8D0E1) main task

![](https://img.shields.io/badge/20220331-FAEFCA) editing info

## Papers
### Survey

1. A Survey of Knowledge-Intensive NLP with Pre-Trained Language Models [[pdf](https://arxiv.org/pdf/2202.08772.pdf)]

summarize the current progress of pre-trained language model based knowledge-enhanced models (PLMKEs) by dissecting their three vital elements: knowledge sources, knowledge-intensive NLP tasks, and
knowledge fusion methods. 
main encyclopedic knowledge-intensive NLP tasks: 
- Open-domain QA
  - Natural Questions
  - HotpotQA
- Fact Verification
  - FEVER
  - BOOLQ
- Entity Linking
  - ACE2004
  - AIDA CoNLL-YAGO
  - WNWI
  - WNCW

### Probing

1. LAMA
2. ParaREL
3. BERT is Not a Knowledge Base (Yet): Factual Knowledge vs. Name-Based Reasoning in Unsupervised QA (preprint)
4. How Can We Know What Language Models Know? (TACL 2020)
5. How Much Knowledge Can You Pack Into the Parameters of a Language Model? (EMNLP 2020)
6. Transformer Feed-Forward Layers Are Key-Value Memories (EMNLP 2021)
7. Knowledge Neurons in Pretrained Transformers (ACL 2022)
8. Transformer Feed-Forward Layers Build Predictions by Promoting Concepts in the Vocabulary Space (preprint)

### Knowledge Retrieving

1. Generalization through Memorization: Nearest Neighbor Language Models (ICLR 2020)
2. REALM: Retrieval-Augmented Language Model Pre-Training (ICML 2020)
3. Adaptive Semiparametric Language Models (TACL 2021)
4. Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks (NeurIPS 2020)
5. Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering (EACL 2021 short)
6. End-to-End Training of Multi-Document Reader and Retriever for Open-Domain Question Answering (NeurIPS 2021)
7. WebGPT: Browser-assisted question-answering with human feedback (preprint)
8. Improving language models by retrieving from trillions of tokens (preprint)
9. Training Data is More Valuable than You Think: A Simple and Effective Method by Retrieving from Training Data (preprint)
10. A Survey on Retrieval-Augmented Text Generation (preprint)

### Knowledge Injection

1. Entities as Experts: Sparse Memory Access with Entity Supervision (EMNLP 2020)
2. Facts as Experts: Adaptable and Interpretable Neural Memory over Symbolic Knowledge (preprint)
3. K-Adapter: Infusing Knowledge into Pre-Trained Models with Adapters (Findings of ACL 2021)
4. Reasoning Over Virtual Knowledge Bases With Open Predicate Relations (ICML 2021)
5. AdapterFusion: Non-Destructive Task Composition for Transfer Learning (EACL 2021)
6. Kformer: Knowledge Injection in Transformer Feed-Forward Layers (preprint)
   
### Model Editing
This section contains the pilot works that might contributes to the prevalence of model editiing paradigm.
1. **Editable Neural Networks** ICLR 2020. ![](https://img.shields.io/badge/Editable_training-DCE7F1) 

   *Anton Sinitsin, Vsevolod Plokhotnyuk, Dmitriy Pyrkin, Sergei Popov, Artem Babenko*.  [[pdf](https://openreview.net/pdf?id=HJedXaEtvS)], [[project](https://github.com/xtinkt/editable)],  2020.7
   ![](https://img.shields.io/badge/image_classification-D8D0E1) ![](https://img.shields.io/badge/machine_translation-D8D0E1)

   Related work:
   - re-train on the original dataset augmented with new samples (expensive)
   - use a manual cache (e.g. lookup table) that overrules model predictions on problematic samples (can't generalize to semantic equivalent inputs)
   Method:
   Editable Training (employ meta-learning techniques to ensure that mistakes can be corrected without harming its overall performance)
   <!-- ![Alt text-w15](editable_train.png) -->

   <img src="img/editable_train.png" width="800" alt="webhooks">


2. **Fact-based Text Editing** ACL 2020. ![](https://img.shields.io/badge/Fact_based_text_editing-DCE7F1) 
   
   *Hayate Iso, Chao Qiao, Hang Li*.  [[pdf](https://aclanthology.org/2020.acl-main.17.pdf)], [[project](https://github.com/isomap/factedit)],  2020.7
   ![](https://img.shields.io/badge/edit_draft_text_editing-D8D0E1) 


   Main cons.:
   - propose a new dataset (task): transforms a draft text into a revised text based on given triples
   - new model, FACTEDITOR. The model consists of three components, a buffer for storing the draft text and its representations, a stream for storing the revised text and its representations, and a memory for storing the triples and their representations
   <!-- ![Alt text-w15](editable_train.png) -->

   <img src="img/fte.png" width="300" alt="webhooks">


 2. Modifying Memories in Transformer Models
   Explicitly modifying specific factual knowledge in Transformer models while ensuring the model performance does not degrade on the unmodified facts.
    - updating stale knowledge
    - protecting privacy
    - eliminating unintended biases (debias)
  #### Baseline
    - Retraining the model on modified training set
    - Fine-tuning on modified facts
    - Fine-tuning on a mixture of modified and unmodified batches

  #### Method
    Constrained fine-tuning on supporting evidences for modified facts

 3. Editing Factual Knowledge in Language Models
   #### Evaluation
    success rate: updates the knowledge
    retain accuracy: retains the original predictions
    equivalence accuracy: for semantically equivalent inputs,
    performance deterioration: test performance deteriorates

 4. Fast Model Editing at Scale
    a model editor efficient: if the time and memory requirements for computing φ and evaluating E are small.
gradients are highdimensional objects 👉 using a low-rank decomposition of the gradient

5. Locating and Editing Factual Knowledge in GPT (preprint)

### Continual Pretraining

1. Don't Stop Pretraining: Adapt Language Models to Domains and Tasks (ACL 2020)
2. Mind the Gap: Assessing Temporal Generalization in Neural Language Models (NeurIps 2021)
3. Towards Continual Knowledge Learning of Language Models (preprint)
4. DEMix Layers: Disentangling Domains for Modular Language Modeling (preprint)
5. Lifelong Pretraining: Continually Adapting Language Models to Emerging Corpora (preprint)
6. Time-Aware Language Models as Temporal Knowledge Bases (preprint)
7. Dynamic Language Models for Continuously Evolving Content (KDD 2021)
8. ELLE: Efficient Lifelong Pre-training for Emerging Data (Findings of ACL 2022)

### Model Editing v.s. Continual Learning
- Common: assimilating or updating a model’s behavior without catastrophic forgetting

- Continual learning: learn a new task while preserving the performance on the previous tasks
wholly new behaviors or datasets
long sequences of model updates

- Model editing: explicitly modifying specific factual knowledge in models while ensuring the model performance does not degrade on the unmodified facts
considers an edit or batch of edits applied all at once
requires the model to memorize new facts that conflict with previously learned facts


