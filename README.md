# POS-with-NetworkX-in-articles

This repo started as a part of the technical assessment for Cyshield, they sent 3 tasks with 14-day time limit, The rest of the tasks will be published as GH repos too for anyone who's interested in looking into them :)

That was the task body:
```
Description
▪Write a pipeline coding of part of speech (POS) tagging that can be represented by network graph .
▪Do pre-processing on the data just to be able to run it.
▪Do optimization time for article to represent every word in article .
▪Feel free to use any technique can help to solve this problem .
✓ U can use Deep Learning Methods and show the diff and which one the best.(optional)
What to turn in:
1) Project documentation (details given below)
2) Report any resource you use
3) Your source code Jupyter Notebook with comment
```

## Dataset
The first thing that I did once I saw that task was to start the dataset hunt, I found 2 good datasets:

Dataset Name | link | main advantage | size
--- | --- | --- | ---
UD_Arabic-PADT | https://github.com/UniversalDependencies/UD_Arabic-PADT | respectful source, already split into training and testing | 6075 samples in train<br>909 in dev dataset<br>680 in test 
Dialectal Arabic Datasets | https://www.kaggle.com/datasets/mahmoudreda55/dialectal-arabic-datasets<br><br>https://huggingface.co/datasets/QCRI/arabic_pos_dialect | contains dialects, already have a benchmark result attached in the dataset document, already uploaded on Kaggle and HF | 350 samples per each dialect: Egyptian, Levantine, Gulf, and Maghrebi<br><br> so 1400 samples in total 

Given its trustworthy source and the fact that it's much bigger, I decided to go with the UD_Arabic-PADT dataset

POS tag | Training freq 
--- | --- 
NOUN  |   74546 
ADP   |  33617 
ADJ   |  23498 
PUNCT |   17511
VERB  |   16807
CCONJ |   15803
X     |   13747
PRON  |    8533
NUM   |   6010
DET   |   4648
SCONJ |   4368
PART  |   1709
AUX   |   1699
ADV   |    880
SYM   |    329
PROPN |    187
INTJ  |    7


## Modelling
I was asked by Cyshield ** What was the biggest challenge you faced when carrying out this project?** to answer this question I would say dealing with Networx, I have never dealt with anything like that before but it's still good to look into it, which is my answer to thier second question **What do you think you have learned from the project?** What I got out of that project was the exposure to a tool like Networx.<br>
I had so much trouble working with the Kaggle notebook, especially when I started using Networx, the notebook kept running out of memory and restarting.

For starting I built a very simple model using the `SimpleRNN` class from `keras` and trained it for only 2 epochs -I tried to go higher but got an overfitting issue- and I got the following results 94.02% training accuracy 93.21% dev accuracy and 90.28% test accuracy.

After that I tried to integrate NetworkX with the RNN Model, The graph representation done by NetworkX was used to create graphs where nodes are tokens and edges represent their connections. The adjacency matrices of these graphs are computed and padded, the model architecture stayed almost the same:
- Embedding Layer: Converts tokens into dense vectors.
- SimpleRNN: Processes token sequences.
- Graph Features: Flattened adjacency matrices are combined with RNN output.
- TimeDistributed Layer: Predicts POS tags for each token in the sequence.
  
This got me 94.67% training accuracy, 93.11% dev accuracy and 92.34% test accuracy, which unfortunately isn't really a great improvement from the baseline.
## Useful references:
- https://medium.com/@tushar_aggarwal/networkx-a-comprehensive-guide-to-mastering-network-analysis-with-python-fd7e5195f6a0
