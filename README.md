# Feature_Importance
Exploring the concept of Permutation Feature Importance

Developing a machine learning model is an iterative process. Often you want to find the most important features in your dataset. If your dataset contains hundreds of features focusing on only the most important can reduce training time and help focus your model. Trying to find the most important features can be like trying to find a needle in a haystack. In your mind you might be thinking, “hey I can quickly find the feature importance by using a random forest model Sklearn and looking at the feature importance attribute”. My response to that is that not all models provide this. We will quickly review a method that regardless of the model used the most important features in the dataset can be found. You only need a fitted model, your dataset, and an evaluation metric.

The intuition behind the method is that you first use your fitted model to predict the target value in your dataset and evaluate how well the model performs using the evaluation metric. This is the baseline. Next one feature of the dataset is randomly shuffled and performance of the predictions of this shuffled dataset is evaluated. The performance of the shuffled column is compared to the baseline. The assumption is that If the feature is not very important to the model, then randomly shuffling up the values will have little impact on the performance of the model. The opposite way of saying this is, if the feature is important then randomly shuffling its values will have a large negative impact in the performance of the model. This random value shuffling is done for all the features of the dataset.

In the linked [Jupyter notebook](https://github.com/stubberf/Feature_Importance), a function is coded that does just that. Starting with the iconic Boston housing dataset, which contains 13 different features, a random forest model trained to predict the median house price. Overall the model performs very well on the test dataset. This fitted model is then passed to a function called “find_feature_importance”. (One quick comment here I am sure there are many ways to code this function. This is just one method to explore this concept.) The function returns a DataFrame where each row contains the name of the feature that was shuffled and the value of the difference in the evaluation metric for the baseline and shuffled feature. The function randomly shuffles each feature by default 10 times.

The process shows that 3 features standout as being the most important to the model.
No alt text provided for this image

![Boxplot of feature importance.](https://media.licdn.com/dms/image/C4E12AQF88hzK7XE0hQ/article-inline_image-shrink_400_744/0?e=1577318400&v=beta&t=EsR2JcTVe3ofQe3BTyUgxw7Q3KmW79Wy18tQqyZfS1s)
- LSTAT = % lower status of the population
- RM = average number of rooms per dwelling
- DIS = weighted distances to five Boston employment centers


A second model was fitted to the same dataset and showed similar values scores for the test set. The most important features for this model are different from the first. The features RM and LSTAT switch for most and second most important features.
No alt text provided for this image

The features TAX (TAX = full-value property-tax rate per $10,000) and PTRATIO (PTRATIO = pupil-teacher ratio by town) become the 3rd and 4th important features.

- TAX = full-value property-tax rate per $10,000
- PTRATIO = pupil-teacher ratio by town

In conclusion the permutation feature importance method is an interesting way of determining the importance of a feature in a model regardless of what type of model it is. This method however is model dependent. The features of a dataset important to one model can be very different for another model. Although this can give some interesting insight on the workings of a model.