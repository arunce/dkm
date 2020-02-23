# When Data that Do Not Conform to Rows and Columns: A Case Study of T-cell Receptor Datasets
###### JARED L OSTMEYER, ASSISTANT PROFESSOR, UT SOUTHWESTERN DEPARTMENT OF POPULATION AND DATA SCIENCES

## Introduction

Statistical classifiers are mathematical models that use example data to find patterns in features that predict a label. Most statistical classifiers assume the features are arranged into rows and columns, like a spreadsheet, but many kinds of data do not conform to this structure. Sequences are one example of a different kind of data, which is why this data is best stored in a text document, not a spreadsheet. To uncover patterns in sequences and other nonconforming features, we have developed a new approach to augment established statistical classifiers with the computational machinery necessary to handle non-conforming features, using what we call *dynamic kernel matching* (DKM).

~~To identify the computaitonal machinery required to handle non-conforming features, the first step is to identify how the features are represented. For example, biological data is often represented as a sequence of symbols. The essential property of a sequence is that both the content and order of symbols provide important information. Sets represent another way data can be structured. A set is like a sequence except the order of the symbols does not encode information. Sometimes non-conforming features are a composite of structures. For example, a patient's immune repertoire is represented a set of sequences. After identifying the structure of how the features are represented, we can implement DKM.~~

We can think of DKM as analogous to the max-pooling operation of a convolutional neural network. Consider the problem of classifying a sequence. Because some sequences are longer than others, the number of features is irregular. Given a specific sequence, the challenge is to determine the appropriate permutation of features with weights, allowing us to run the features through the statistical classifier to generate a prediction. To find the permutation of features that will exhibit the maximal response, like how max-pooling identifies the image patch that will exhibit the maximal response, we use a sequence alignment algorithm. Given the immense number of possible permutations, the problem appears computationally complex but can be solved in polynomial time using a sequence alignment algorithm, like the Needleman-Wunsch algorithm [(link)](https://en.wikipedia.org/wiki/Needleman–Wunsch_algorithm). The equivalent of a sequence alignment algorithm exist for (i) sets, (ii) trees, and (ii) graphs, allowing us to use DKM for non-conforming features represented using these structures. Unfortunately, the general problem of graph alignment is considered NP-hard.

To illustrate the problems we can handle with DKM, we consider two datasets of T-cell receptors, anticipating these datasets to contain signatures for diagnosing disease. The following two T-cell receptor datasets provide distinct examples of non-conforming data.

![alt text](artwork/data.png "Layout of data used in this study")

10x Genomics has published a dataset of sequenced T-cell receptors labelled by interaction with disease particles, which are called antigens [(link)](https://www.10xgenomics.com/resources/application-notes/a-new-way-of-exploring-immunity-linking-highly-multiplexed-antigen-recognition-to-immune-repertoire-and-phenotype/). We refer to this as the antigen classification dataset. See the folder `antigen-classification-problem` for instructions to setup the dataset and fit a multinomial regression model augmented with DKM to solve the antigen classification problem.

Adaptive Biotechnologies has published a separate dataset of patients' sequenced T-cell receptors, which are called immune repertoires, labelled by those patients' CMV status [(link)](https://clients.adaptivebiotech.com/pub/emerson-2017-natgen).
We refer to this as the repertoire classification dataset.
Training data is used to fit a model, validation data is used for model selection, and test data is for reporting results. All results on test data must be reported. See the folder `repertoire-classification-problem` for instructions to setup the dataset and fit a logistic regression model augmented with DKM to solve the repertoire classification problem.

Training data is used to fit a model, validation data is used for model selection, and test data is for reporting results. We strictly adhered to this protocol, ensuring that we avoid a model selection bias during this study.

## Requirements

* [Python3](https://www.python.org/)
* [TensorFlow == v1.14](https://www.tensorflow.org/)
* [NumPy](http://www.numpy.org/)
* [h5py](https://www.h5py.org/)

## Recommended Tools

* [HDF5 Database Viewer](https://www.hdfgroup.org/downloads/hdfview/)

## Download

* Download: [zip](https://github.com/jostmey/dkm/zipball/master)
* Git: `git clone https://github.com/jostmey/dkm`
