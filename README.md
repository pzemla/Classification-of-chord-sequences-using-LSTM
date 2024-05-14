[![pl](https://img.shields.io/badge/język-PL-red.svg)](https://github.com/pzemla/Classification-of-chord-sequences-using-LSTM/blob/main/README.pl.md)
# Classification of chord sequences using LSTM

**How to run**
1. Make sure files train.pkl and test.pkl are together in directory with LSTM.ipynb
2. Run LSTM.ipynb in Jupyter Notebook


**Dependencies**

Python 3.9.13

matplotlib 3.8.3

notebook 7.1.2

numpy 1.24.1

pandas  2.2.1

scikit-learn 1.4.1.post1 Python 3.9.13

torch 2.2.1+cu118

## Overview

The goal of this project is to build a Long Short Term Memory (LSTM) neural network to classify sequences into one of 5 classes. LSTM is implemented using Python with the Pytorch library. This project serves as an educational exercise and practical application of deep learning techniques to sequence classification tasks.

The training and test data are chord sequences with the assigned composer of a chord sequence saved in a pkl file. The goal of the network is to classify sequences into the appropriate composer.

The number of sequences per composer is unbalanced (as shown in histogram below), making the network difficult to train as it tends to classify all sequences into one class/composer. In order to train the network more balanced, weights were assigned to classes based on their number of sequences (the fewer sequences a class has, the bigger weight assigned to it). 

![image](https://github.com/pzemla/Classification-of-chord-sequences-using-LSTM/assets/135070990/fa600388-5e6b-44b6-a052-e98630cbc7c7)

LSTM network was used because the data is sequential data, making various types of recurrent neural networks out of simpler neural networks types, and LSTM pays equal attention to each element of the sequence, regardless of whether it is at the beginning, middle or the end of the sequence (as opposed to a regular recurrent neural network).

Data before pre-processing (sequence and assigned class): 
 
(array([ -1., -1., -1., ..., 78., 40., 144.]), 0)

(array([ -1., -1., 144., ..., 32., -1., -1.]), 0) 

## Optimizer and loss function

Optimizer – Adam (learning rate=0.0001) 

Loss function – Cross-entropy loss 

The Adam optimizer was chosen because it dynamically adjusts the learning rate to each parameter during training, so there is no need to adjust the learning rate decay. Out of all optimizers tested 
(Adagrad and RMSprop), it provided the best results in the test dataset. 

The cross-entropy loss function was chosen because its result can be interpreted as the probability of belonging to each class, which is why it is often used for classification models. 

## Results

Accuracy: 70% 

Accuracy of individual classes: 81% 61% 28% 67% 45% 

Average class accuracy: 57%

While overall accuracy is relatively high, accuracy of every individual class varies depending on number of sequences in class data. Without added weights to each class, LSTM classified most of sequences into first class, which achieved high accuracy, but average class accuracy was only around 20% (100% for first class, 0% for all others). Accuracy of individual classes could be further improved by increasing class weights, so that classes with less data have higher impact during training. Other possible method could be equalizing quantity of data in all classes, either by decreasing amount of chord sequences in first class, or duplicating them in other classes with less data.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
