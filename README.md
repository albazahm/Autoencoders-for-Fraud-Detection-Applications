# Autoencoders-for-Fraud-Detection-Applications
An assignment for the Lantern Institute exploring the use of Autoencoders in fraud detection applications.

This notebook explores the use of autoencoders as a step in approaching classification in imbalanced datasets.

Fundamentally, autoencoders are neural networks that take data as their input and attempt to reconstruct that data as it's output. This by having a hidden layer(s) of smaller size than the input. This will allow the model to learn a compressed, more concise representation of the input features with fewer dimension that the input. These compressed features translate to the non-linear combination of the input features that are characteristic of the input and the most useful in in the reconstruction of the data. The model will then use those features to reconstruct the input.

So why would would we want to recreate the input? What does this have to do with classification in imbalanced datasets?

The problem with imbalanced datasets is that even a very simple classifier can achieve high accuracy score by all observations as the majority class. If a dataset has 90% class A and 10% class B with the model predicting class A for all observations, then the model will still achieve a 90% accuracy. The model hasn't really learned anything about the data and is just taking advantage of the disproportionate representation of the classes. This shows a failure of some models in handling imbalanced datasets as well as the failure of accuracy as a metric in evaluating models that deal with imbalanced datasets.

For the first problem oversampling of the majority class, undersampling of the minority class, or both can help achieve balance in the number of observations of each class. Many models also allows for class weight parameters that assign more weight to misclassification of the minority class to pressure the model to learn how to classify it better. Strategies to tackles the second problem include using precision, recall and f1-scores in conjunction to score, tune and evaluate a model.

Which brings us to autoencoders. If we train an autoencoder on ONLY the features of the majority class in a binary classification, the model will learn a characteristic representation of the precitor features of that class and how to reconstruct it. Since the model has only seen the majority class thus far, it should theoretically be able to reconstruct that data with a lower error than any unseen data. As a result, when the autoencoder is fed the data from the minority class, it will reconstruct it with a higher error. By exploring the difference in that reconstruction error we should be able to tell which class an observation belongs.

Let's explore a use case for this in Fraud Detection Analytics. When developing fraud detection algorithms, companies have access to large amounts of transactional data, most of which belongs to legitimate/normal transactions. They have relatively few data points corresponding to fraudulent transactions which pose a challenge in developing the algorithms to detect them for the reasons discussed above.

The dataset for fraud detection is provided by Kaggle: https://www.kaggle.com/mlg-ulb/creditcardfraudT
