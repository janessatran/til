## Machine Learning Methods for Survey Researchers
source: [https://www.surveypractice.org/article/2718-an-introduction-to-machine-learning-methods-for-survey-researchers](https://www.surveypractice.org/article/2718-an-introduction-to-machine-learning-methods-for-survey-researchers)

### Common Example Description
*	Goal: predict simulated binary response outcome using various predictors in NHIS dataset
  *	Dataset: 26,785 adults age 18+, region, age, sex, education, race, income level, Hispanicity, employment status
* Binary survey response variable randomly generated from simulated probit model (nonlinear function of demographic variables)
  *	**probit model**: type of regression where dependent variable can take only two values, for example, married or not married
* For evaluation, they used a split sample cross-validation approach 
  *	Training data set: 85%
  *	Test data set: 15%
  *	Accuracy metrics: percent correctly classified, sensitivity, specificity, balanced accuracy (average of sensitivity and specificity), and AUC
    * Sensitivity: aka true positive rate, measures the proportion of actual positives that are correctly identified; calculated as true_positive / (true_positive + false_negative)
    *	Specificity: aka true negative rate, measures the proportion of actual negatives that are correctly identified; 
    *	Fall-out: aka false-positive rate; calculated as false_positive / (false_positive + true_negative)
    
### AUC
Measures area underneath the ROC Curve
* **ROC curve**: graph showing performance of a classification model at all classification thresholds; False Positive Rate vs True Positive Rate;  roc stands for Receiver Operating Characteristic
*	Provides an aggregate measure of performance across all possible classification methods
*	It can be interpreted as the probability that the model ranks a random positive example more highly than a random negative example
*	For example, given the following results which are arranged from left to right in ascending order of logistic regression predictions, AUC represents the probability that a random positive (green) example is positioned to the right of a random negative (red) example 

[img]()

* AUC ranges in values from 0 to 1, a model whose predictions are 100% wrong has an AUC of 0.0, while a model whose predictions are 100% correct has an AUC of 1.0
* It is desirable as a measure of accuracy for the following reasons: 	
  *	It is **scale-invariant**: it measures how well predictions are ranked, rather than their absolute values
  *	It is **classification-threshold-invariant**: it measures the quality of the model’s predictions irrespective of what classification threshold is chosen
    *	Not so great in cases where there are wide disparities in the cost of false negatives vs false positives (e.g. when doing email spam detection, you likely want to prioritize minimizing false positives even if that results in significant increase of false negatives) 
