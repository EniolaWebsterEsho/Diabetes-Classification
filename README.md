# Diabetes-Classification

A.	Title
Pima Indians Diabetes Database. This dataset is from the National Institute of Diabetes and Digestive and Kidney Diseases and released by Johns Hopkins University.

B.	Data description
There are number of 768 instances and 8 attributes with Class. All the attributes are numeric and the Class is categorical. The attributes are listed below:
1. Number of times pregnant
   	2. Plasma glucose concentration a 2 hours in an oral glucose tolerance test
   	3. Diastolic blood pressure (mm Hg)
  	4. Triceps skin fold thickness (mm)
  	5. 2-Hour serum insulin (mu U/ml)
 	6. Body mass index (weight in kg/(height in m)^2)
   	7. Diabetes pedigree function
   	8. Age (years)
 	 9. Class variable (0 or 1)
Several constraints were placed on the selection of these instances from a larger database.  In particular, all patients here are females at least 21 years old of Pima Indian heritage.

C.	Task
Classify a person tests positive or negative for diabetes based on the 8 attributes.

D.	Data Information
The figure below shows the first five information of the diabetes dataset (diabetes.head()).

![image](https://user-images.githubusercontent.com/91756330/209987525-db573df0-01e9-4421-873b-dc40dbc24fe9.png)

E.	Data Visualization
The best way to start the analysis is visualizing the dataset. Below is the histogram plot showing the distribution count of each attribute. 

![image](https://user-images.githubusercontent.com/91756330/209987570-9a875b3a-6a90-48b3-aac6-7bcceb8a066b.png)

 Also, the correlation between each attributes can be visualized using heatmap. From the output, the lighter colors indicate more correlation. There is correlation between pairs of features, like age and pregnancies, or BMI and skin thickness, etc.
 
![image](https://user-images.githubusercontent.com/91756330/209987656-249bf3ea-b4fd-49bc-86cd-f3dad3d822bf.png)

F.	Data Cleaning
First, I checked for missing values using the isnull().sum() function.
 
![image](https://user-images.githubusercontent.com/91756330/209987754-89f00642-4bbf-40f7-9818-6118bae740b5.png)

Initially, it seems there is no missing value but Glucose, Blood Pressure, Insulin, Triceps Skin Thickness and BMI contain a value of 0 which may represent the missing value. For example, a person's glucose or insulin value cannot be 0. Considering this situation, let's assign the 0 values to the relevant values as NaN and then apply the operations to the missing values. However, the pregnancy value can be 0 so it is excluded from the NaN.
 
![image](https://user-images.githubusercontent.com/91756330/209987790-e1a06ee9-a827-46d1-8252-468dbbaac4d1.png)

Then, the NaN values are replaced with the mean value using the simple imputer from sklearn.

![image](https://user-images.githubusercontent.com/91756330/209987845-1755b9e7-75c7-446c-bc6c-ab724d88bd89.png)

For the Class categorical attribute, one hot encoding is used to change the outcome from “tested_negative” and “tested_positive” to 0 or 1. 

![image](https://user-images.githubusercontent.com/91756330/209987882-fc56be9a-56b1-46d3-8d60-032351382775.png)

G.	Data Preprocessing
Before implementing classification algorithm, the dataset is scaled using sklearn’s MinMaxScaler() function. This function transform features by scaling each feature to a given range. 

![image](https://user-images.githubusercontent.com/91756330/209987939-7aa37ae7-0c37-42e0-b2f8-90b92091e3a8.png)

H.	Train Test Split
Using sklearn’s train_test_split, the feature (X) and target (y) dataframes is split into a training set (80%) and testing set (20%). Training set is used for building classification models and testing set is used for evaluating the performance of the model.
 
![image](https://user-images.githubusercontent.com/91756330/209987993-15075a41-7d75-4f82-8481-bd345fbbad49.png)

![image](https://user-images.githubusercontent.com/91756330/209988034-75581153-07d9-4219-b977-baa21eaae76e.png)

I.	Justification

1.	Decision Tree Classifier
* It can handle various data type i.e. discrete or continuous values.
* 	Requires little or no data preparation.
2.	Logistic Regression
* Used for binary response i.e. it has only two possible outcomes (e.g. 0 or 1). 
* Easy to implement, interpret, and very efficient to train.

J.	Decision Tree Classifier Performance Evaluation and Result
From sklearn metrics, the accuracy score, confusion matrix and classification report were imported for the model performance evaluation.
1.	Accuracy Score 

![image](https://user-images.githubusercontent.com/91756330/209988139-2ef46622-9bb1-43ab-80d2-bd34c2c332da.png)

2.	Confusion Matrix
 
![image](https://user-images.githubusercontent.com/91756330/209988186-8054fec4-6eca-4ce7-87fc-1fe0b0dba4ca.png)
 
True Positives (TP [1, 1]): the model correct prediction of people that have diabetes = 32
True Negatives (TN [0, 0]): the model correct prediction of people that don’t have diabetes = 88
False Positives (FP [0, 1]): the model incorrect prediction of people that do have diabetes (a "Type I error") = 19
False Negatives (FN [1, 0]): the model incorrect prediction of people that do not have diabetes (a "Type II error") = 15

3.	Classification Report 

![image](https://user-images.githubusercontent.com/91756330/209988247-b0d0966e-0f67-4a6d-b9bd-1d7333229cd7.png)

•	Precision is the accuracy of positive predictions. Precision = TP/ (TP + FP). The model has a high precision of 0.85 and 0.63. 
•	Recall is the fraction of positives that were correctly identified. Recall = TP/ (TP+FN). The model has a high recall of 0.82 and 0.68.
•	The F1 score is a weighted harmonic mean of precision and recall such that the best score is 1.0 and the worst is 0.0. The model F1 score is 0.84 and 0.65.
•	Support is the number of actual occurrences of the class in the specified dataset.

K.	Logistic Regression Performance Evaluation and Result
1.	Accuracy Score
 
![image](https://user-images.githubusercontent.com/91756330/209988292-0d953901-a04b-4d7c-ba98-3217788c0cb3.png)

2.	Confusion Matrix

![image](https://user-images.githubusercontent.com/91756330/209988336-db2ff1ca-b379-4892-aeb5-2bda5c3f77ba.png)

True Positives (TP [1, 1]): the model correct prediction of people that have diabetes = 27
True Negatives (TN [0, 0]): the model correct prediction of people that don’t have diabetes = 99
False Positives (FP [0, 1]): the model incorrect prediction of people that do have diabetes (a "Type I error") = 8
False Negatives (FN [1, 0]): the model incorrect prediction of people that do not have diabetes (a "Type II error") = 20
3.	Classification Report 

![image](https://user-images.githubusercontent.com/91756330/209988380-bfa19826-74f0-4d8b-9ffb-79b170c74ec1.png)

•	Precision is the accuracy of positive predictions. Precision = TP/ (TP + FP). The model has a high precision of 0.83 and 0.77. 
•	Recall is the fraction of positives that were correctly identified. Recall = TP/ (TP+FN). The model has a high recall of 0.93 and 0.57.
•	The F1 score is a weighted harmonic mean of precision and recall such that the best score is 1.0 and the worst is 0.0. The model F1 score is 0.88 and 0.66.
•	Support is the number of actual occurrences of the class in the specified dataset.

L.	Conclusion
Decision tree classifier and logistic regression models were able to perform well with accuracy of 77.92% and 81.82% respectively. However, the logistic regression performed better than the decision tree and therefore it is a better classification model for this dataset.
