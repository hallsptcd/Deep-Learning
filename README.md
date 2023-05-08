# Deep Learning

**Language**: Python.

**Introduction**: 

The aim of this project is to investigate a number of Deep Learning methods in the context of text processing and text classification. This task uses a dataset of articles extracted from The Guardian newspaper, and aims to predict the broader section from which an article was taken.

The dataset, taken from Kaggle, contains 148,731 newspaper articles scraped from The Guardian website, and dating from between January 2016 and June 2022. In the original dataset, there were 159 sections. Quite a number of the original sections contained very few articles, and had oddly specific titles. I have chosen to remove these sections, and to focus on the four most popular: Football, Opinion, Sport, and World News. By narrowing the focus to these four sections, we can still investigate the ability of the models to discern text from related as well as from distinct sections, but we maximise the number of available training examples for each section, which is important for machine learning in general and neural networks in particular. This also permits us to solve the slight imbalance problem through under-sampling while still preserving a sizeable dataset.

It is necessary to convert the raw text data into a form which can feed into a deep network. This will require both the input and label data to be transformed. In general, pre-processing required on-the-fly text embedding and label encoding. Lastly, the data was partitioned in the normal way into a training, validation, and test set. The accuracy, and other metrics which are presented throughout this report, will refer to predictions made using the unseen data in the test set.

The pre-processing of the input data also included the selection of a number of parameters. These parameters were standardised to allow for effective comparison among models. Ultimately, these were chosen through a combination of grid-search and trial-and-error. One of these parameters relates to padding, and dictates the maximum and minimum length of the input sequence representing each article. This was set to 250. Another parameter, this time setting the maximum size of the vocabulary of words, was set to 1500. Finally, the dimensionality of the on-the-fly embedding vectors was chosen to be 8. Naively, an increase in these numbers might be expected to increase the accuracy of the models as they are permitted to capture more information, but experiment yielded little improvement. This, as always, must also be balanced against the use of more computational resources and a longer training process.

Next, we build the model. The optimum architecture was a hybrid CNN-LSTM model with an embedding layer, two CNN layers (the first with 256 filters and a kernel of size 4, and the second with 64 filters and a kernel of 8) with two intermediate pooling layers, then two LSTM layers (the first with state size of 16 and the second of 32), a hidden layer with 350 neurons, and an output layer with a softmax activation function, since each article will be classified with a single label. I opted for a Categorical Crossentropy loss function, the adam optimiser, and accuracy as our primary evaluation metric. In addition, we also employ dropout, regularisation, and early-stopping to prevent overfitting.

**Data Files**: 

The Guardian Article dataset comes from here: https://www.kaggle.com/datasets/adityakharosekar2/guardian-news-articles
