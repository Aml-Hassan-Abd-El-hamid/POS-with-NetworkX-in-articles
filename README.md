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
The first thing that I did once I saw that task was starting the dataset hunt, I found three datasets:

Dataset Name | link | main advantage | size
--- | --- | --- | ---
UD_Arabic-PADT | https://github.com/UniversalDependencies/UD_Arabic-PADT | respectful source, already split into training and testing | 6075 samples in train<br>909 in dev dataset<br>680 in test 
Dialectal Arabic Datasets | https://www.kaggle.com/datasets/mahmoudreda55/dialectal-arabic-datasets<br><br>https://huggingface.co/datasets/QCRI/arabic_pos_dialect | contains dialects, already have a benchmark result attached in the dataset document, already uploaded on Kaggle and HF | 350 samples per each dialect: Egyptian, Levantine, Gulf, and Maghrebi<br><br> so 1400 samples in total 

Given its trust-worthy source and the fact that it's much bigger, I diceided to go with the UD_Arabic-PADT dataset

POS tag | training freq | desc
--- | --- | --- 
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

Given the fact that in many cases, the POS tag of the token depends on how it appears in the sentence - 1584 tokens happen to be labelled with different POS tags -, that problem can be defined as a sequence problem - most NLP problems are so LOL - so I had to pick up a sequential model to deal with the problem.

**LSTM**<br> 
I tried simple LSTM models with variant hyper-parameters -including #nodes, batch_size, and #epochs- and  the best that I got was 79.69% training accuracy 81.92% dev accuracy and 69.09% test accuracy<br>

I tried the same simple LSTM models with variant hyper-parameters and the best that I got was 93.42% training accuracy 93.25% dev accuracy and 90.45% test accuracy.<br> 

The only difference between the first batch of experiments and the second ones was the `maxlen` provided to the `pad_sequences` function, as in the first no.of experiments `maxlen = 150` and in the second batch of experiments  `maxlen = 478` where 478 is the length of the biggest sequence in the training dataset.

**RNN**<br>
I built a very simple model using the `SimpleRNN` class from `keras` and trained it for only 2 epochs -I tried to go higher but got an overfitting issue- and used the same `maxlen` as in LSTM and I got the following results 94.02% training accuracy 93.21% dev accuracy and 90.28% test accuracy.

## Useful references:
- https://machinelearningmastery.com/understanding-simple-recurrent-neural-networks-in-keras/
- https://medium.com/@tushar_aggarwal/networkx-a-comprehensive-guide-to-mastering-network-analysis-with-python-fd7e5195f6a0
