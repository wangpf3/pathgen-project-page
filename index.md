## Motivation

Commonsense question answering requires general background knowledge which is not explicitly stated in the given context. 
Prior works rely on existing knowledge graphs (KGs) to obtain their knowledge for reasoning.
However, these KGs are not completed and may not contain the knowledge necessary to answer a question.

## Our method
In this work, we augment a general commonsense QA framework with a **knowledgeable path generator**.
As depicted in the figure below,
we firstly extract a pair of entities mentioned in the context (step 1).
Then our generator outputs a potentially novel, multi-hop relational path to connect them (step 2).
Later, all such paths serve as structured evidence for solving commonsense questions (step 3).

![Image of pipeline](https://github.com/wangpf3/pathgen-project-page/blob/gh-pages/pipeline.png?raw=true)

## How to learn such a path generator?
1. Sample a set of relational path from a commonsense KG with random walk. We adopt some heuristic strategies to ensure the relevance and informativeness
of the paths.
- **Relevance**: We filter out a subset of relational types that we assume to be unhelpful for answering commonsense questions, e.g., RelatedTo, prior to sampling.
- **Informativeness**: We require all relations types in a path to be distinct so it would not be trivial.

2. Fine-tune a pretrained language model --GPT-2 on the sample paths. This would transfer the rich knowledge encoded in GPT-2 to our path generator for combatting 
the sparsity of KGs.

## Path generator as a plug-in for other knowledge-intencive tasks
If you would like to try out our path generator to provide structured knowledge for other downstream tasks,
you can find how to use it as a plug-in module in our [notebook](https://github.com/wangpf3/Commonsense-Path-Generator/blob/main/A-Commonsense-Path-Generator-for-Connecting-Entities.ipynb). We also provide a well-trained generator checkpoint to [download](https://drive.google.com/file/d/1dQNxyiP4g4pdFQD6EPMQdzNow9sQevqD/view?usp=sharing).


## Experiments
We conduct extensive experiments on both [OpenBookQA](https://leaderboard.allenai.org/open_book_qa/submissions/public) and [CommonsenseQA](https://www.tau-nlp.org/csqa-leaderboard), which demonstrate the effectiveness of our method in improving previous systems with static KG (by up to 6% in accuracy).
Experiments in low-resource setting also show the rubustness of our method to less training data.


## To cite
```
@article{wang2020connecting,
  title={Connecting the Dots: A Knowledgeable Path Generator for Commonsense Question Answering},
  author={Wang, Peifeng and Peng, Nanyun and Szekely, Pedro and Ren, Xiang},
  journal={arXiv preprint arXiv:2005.00691},
  year={2020}
}
```
