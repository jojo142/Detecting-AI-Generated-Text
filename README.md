# Large Language Models: Detecting-AI-Generated-Text

### Problem
We chose the Kaggle Competition, Large Language Models - Detect AI Generated Text as our problem to solve. In recent years, large language models (LLMs) have become increasingly sophisticated, and are now capable of generating text that is difficult to distinguish from human-written text. This creates concerns about plagiarism in educational settings such as schools, and can be used as a shortcut by students to complete assignments without effort, which can be detrimental to their education. We chose this topic because we see the value in creating a model that can distinguish between student-written essays and those generated by AI that will essentially contribute to ensuring the responsible use of AI within academic settings.

The goal of this competition was to develop a machine learning model that can accurately detect whether an essay was written by a student or an LLM. The train dataset provided by the competition was composed mainly of a mix of middle and high school student-written essays and a few essays generated by a variety of LLMs along with their correct labels. The testing dataset was hidden by the competition, used to evaluate the model when submitting a prediction.

Our planned solution was a multi-faceted approach that aimed to address the unique challenges posed in the distinguishing of human-written text and AI-generated text in the context of educational settings. The comprehensive feature engineering, model selection, and evaluation strategies were designed to contribute to the responsible use of AI in academia.

### Method
Our method involved a comprehensive approach:

- **Data Loading:** We utilized the `sklearn` libraries to efficiently load and manage the dataset.
- **Feature Engineering:** Leveraging the `TextBlob` library, we performed sentiment analysis and other textual analyses to extract features such as part-of-speech tagging, sentence length, and sentiment scores.
- **Data Splitting:** Using the `train_test_split` function, we split the training data into a training set and a validation set, ensuring a robust evaluation of our models.
- **Text Vectorization:** To convert the textual data into a format suitable for machine learning models, we used the `CountVectorizer` to create a Bag of Words representation.
- **Model Selection and Training:** We tried a Logistic Regression model due to its simplicity and effectiveness in binary classification tasks. Additionally, we experimented with other models, including Support Vector Machines (SVM) with a linear kernel and XGBoost, aiming to identify the most suitable model for the task.
- **Model Evaluation:** We assessed the performance of our models using the `roc_auc_score` from `sklearn.metrics`, since this was the evaluation method of the competition.
- **Ensemble Method:** To enhance predictive accuracy, we explored ensemble techniques such as a Voting Classifier, combining the strengths of Logistic Regression, SVM, and XGBoost.
- **Hyperparameter Tuning:** To optimize model performance, we experimented with tuning hyperparameters and adjusting learning rates.
- **Analysis and Future Directions:** Following model evaluation, we conducted a thorough analysis, identifying the strengths and weaknesses of each model. We also outlined potential future directions, such as the exploration of external data and advanced modeling techniques to further improve our model's accuracy.
---
With the real test set being hidden during the model development process, we let the models predict the probabilities of the essays being AI-generated rather than human-written through predictions using the validation set that we split from the train data provided by Kaggle, and used this for measuring the accuracy of our models. With the accuracy statistics from this step, we cross validated using different models with the validation set to seek reliable model performance. Afterwards, we also attempted to use the Ensemble Bagging method to combine our models and get more accurate results. Lastly, we checked for any possibilities for overfitting, to ensure that our models would perform well with the hidden test data as well.

Our final step was to make predictions on the test set. The test set, concealed during model development, serves as a real-world evaluation to gauge how well our models generalize to unseen data. These predictions were submitted to the competition platform, Kaggle, for official evaluation and ranking. Our comprehensive approach encompassed training, validation, and testing stages, emphasizing robustness and accuracy to contribute to the goal of ensuring the responsible use of AI in academic settings.

### Experiments
We undertook a meticulous feature engineering process to enhance the predictive power of our models. Initially, we employed sentiment analysis using the `TextBlob` library to extract sentiment polarity from each essay in order to quantify the emotional tone present in the text. Subsequently, the essays underwent transformation into a matrix of token counts through the application of the `CountVectorizer` from `sklearn`, adopting the Bag of Words model to capture word frequency in the document. Additional features, including average sentence length, word count, and n-gram features, were incorporated to provide a fuller representation of the essays.

#### Visualization of Features
- As average sentence length increased, the word count also increased. This suggests a strong, positive correlation between longer essays and longer average sentence length.
![HfkYBXYlIyog8SskFsrLkYH2kaPHTe_RUbArj7fofmpf3_EjJCeIA6Zk6OubpLIKDCe5HoLKmJtPTFUVyGonC0PUDRc7h4SxuAg3-ZQusUAdSTboZGrqlOEvz_Vl](https://github.com/jojo142/Detecting-AI-Generated-Text/assets/76130563/0779f547-7b96-4874-9825-e61a89a2a752)


- Most train essays had a neutral or positive sentiment score, and the most frequent scores were around 0.1 to 0.2.

![8iqxBQ6AAKxlurDx_I2Ct2zUxSH1EuOYetEokBjNWwnR1VToBQS6YeDW9MI6X1ruCRD8Y8c6cAzZcJWnWLOleitMdABW0pNCTMzEmI44FD8A2gznRjzaRDJJPuN7](https://github.com/jojo142/Detecting-AI-Generated-Text/assets/76130563/2654d72b-19ad-4c65-907a-c0320c2541f7)

- This plot illustrates how a majority of the train essays were predicted to be human-written even across a wide range of sentiment scores, which makes sense because the data were mostly composed of human-written essays. Those predicted to be written by AI tended to have a higher sentiment score.
![1wyHHl-d7MAdjAEpodsbEQ-9QCqnQUEEoSb6KcqoevPmjxTK_vY5XJy5VaOVtqAo1lvoLfdZ4A_RNVmezapRxgoiTVOtfNZ4u6P6_kUn0GXaxoXOmFQ_lRWO5XCE](https://github.com/jojo142/Detecting-AI-Generated-Text/assets/76130563/fe7b8797-bd60-4797-9fca-e43320f28c85)

- For the voting classifier model, the sentiment analysis feature had the largest positive impact on ROC AUC score when compared to the other features.
<img width="478" alt="0FeHSn3w0fHLEazlB_EUGdbFYQBAz9kIQ2GOskHqXMCecyCMsC-3mG7D6CcKH-NvhrPhdR_185EnYIaQ5AkzXeP43V4NqGVmEdi4IifWk1liFg3TWQgnAMi4Z5oz" src="https://github.com/jojo142/Detecting-AI-Generated-Text/assets/76130563/eadb0e1d-38c6-43b1-a675-4232dfd9a4af">

### Models
Moving on to model selection, we chose Logistic Regression for its simplicity and effectiveness in binary classification tasks. Initially, to enhance predictive capabilities, we integrated sentiment analysis, producing a public score of 0.553. The dataset underwent extensive feature engineering, incorporating sentiment scores, average sentence length, word count, and n-gram features. This comprehensive feature set aimed to capture nuanced patterns within the text data. Despite a convergence warning during training, the logistic regression model demonstrated strong predictive power on the validation set, showcasing high ROC AUC, accuracy, precision, and recall. Insights provided by the confusion matrix and classification report highlight the model's robust performance across various metrics. The model achieved a noteworthy ROC AUC score of 0.9709 on the validation set. We can further optimize the model by fine-tuning hyperparameters and exploring additional features to refine its effectiveness.

For the support vector machine (SVM), while multiple kernels were experimented with during the model development progress (including the linear kernel, polynomial kernels of degree 3 and 4, and the radial basis function (RBF) kernel), the SVM with a linear kernel was employed as it came out on top with the best accuracy compared to all other kernels, showcasing superior performance with a high ROC AUC score of 0.9891 on the validation set. We used average sentence lengths of the essays as a feature for this model to make judgements.

<img width="716" alt="Screenshot 2023-12-18 at 10 45 51 PM" src="https://github.com/jojo142/Detecting-AI-Generated-Text/assets/76130563/8cdf9264-c9dd-48a1-8d04-78c2118c0062">

The third model we decided to try was XGBoost, which uses gradient boosting and the ensemble method for supervised learning. The XGBoost model, known for its efficiency, contributed positively with a ROC AUC score of 0.9873 on the validation set. While developing this model, we tried converting the essays to numerical data using the TF-IDF vectorizer, which places importance on word relevance to the corpus, not just word frequency. We also experimented with considering different ranges of ngrams to keep word context and eliminated common stop words before vectorization. We found that adjusting the learning rate to 0.0001 improved the public score by a small amount. 

<img width="765" alt="-gwreD5KRRC4YCWjn1LYaSdplz_ShZ81PERkLEudPJmbHR_e9cfJpZIh3TjGmAAw1fL0VCKN6HpfeOjGETel6D14Bo7hTdWw_T0aT37agAnnvevA3c9jBCblkawn" src="https://github.com/jojo142/Detecting-AI-Generated-Text/assets/76130563/f25b112d-cedc-4e62-8633-7db0a6162eee">

Recognizing the complementary strengths of individual models, we implemented a soft voting classifier as part of an ensemble approach. This classifier combined the logistic regression, SVM, and XGBoost models, showcasing a competitive ROC AUC score of 0.9855 on the validation set. The ensemble method demonstrated the effectiveness of leveraging diverse models to achieve a more balanced and accurate prediction.

### Conclusion 
Out of the models we used, the SVM with a linear kernel gave the highest accuracy score of 0.602 in our Kaggle submissions (a somewhat expected result with how SVM’s model is intended to be used for classification tasks), followed by Logistic Regression (0.553) and finally XGBoost (0.506). However, the accuracy scores were still low compared to submissions from other competitors.
Through investigation of why this was the case, we were able to evaluate that this gap in accuracy score with other competitors was mainly due to the difference in the datasets that were used to train our models, and the use of advanced modeling techniques. However, we can predict that the models we built could have similar performance if given the same datasets to train with. Other competitors utilized external data and extra generated essays to train their models, while we used only the essays provided by Kaggle to train ours.

Kaggle was unable to receive our predictions using the ensemble method due to a long runtime and large CPU usage when running with the hidden test data. However, we can conclude that the ensemble method would provide effective performance if we could use it for our predictions on the test data, based on the results we had found from running it using the train data. 



