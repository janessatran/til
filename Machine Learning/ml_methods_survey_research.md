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

<img src="https://developers.google.com/machine-learning/crash-course/images/AUCPredictionsRanked.svg">

* AUC ranges in values from 0 to 1, a model whose predictions are 100% wrong has an AUC of 0.0, while a model whose predictions are 100% correct has an AUC of 1.0
* It is desirable as a measure of accuracy for the following reasons: 	
  *	It is **scale-invariant**: it measures how well predictions are ranked, rather than their absolute values
  *	It is **classification-threshold-invariant**: it measures the quality of the model’s predictions irrespective of what classification threshold is chosen
    *	Not so great in cases where there are wide disparities in the cost of false negatives vs false positives (e.g. when doing email spam detection, you likely want to prioritize minimizing false positives even if that results in significant increase of false negatives) 

## Using Support Vector Machines for Survey Research
Source: [https://www.surveypractice.org/article/2715-using-support-vector-machines-for-survey-research](https://www.surveypractice.org/article/2715-using-support-vector-machines-for-survey-research)

*	**Support Vector Machines (SVM)**: classify binary outcomes (e.g. survey responses vs nonresponse) by estimating a separation boundary within space defined by set of predictor variables
*	In the simplest case, SVMs create a **“maximal margin”** in the predictor space – the largest buffer separating observations for one outcome from those of the other outcome
 *	Cases that fall exactly on the margin are called support vectors because these specific cases alone define the unique boundary solution
*	If there are two predictor vars, the separating boundary is a line
 *	Three -> a plane
 *	More than three -> separating hyperplane
*	Predictors are obtained from SVMs by using the corresponding decision function that is a mathematical depiction of the boundary

Example: suppose a researcher wants to predict survey participation based on age (X1) and income (X2)
*	Possible labels: survey respondents (red triangles) and survey non-respondents (blue circles)
*	Optimal hyperplane (aka boundary) separating respondents from non-respondents is line labeled H (this is the simplest case)
*	Classification boundary is “optimal” in that it minimizes the classification error in the training data set
* The maximal margin classifier finds the maximal margins, such that the resulting separating hyperplane H is farthest from the training observations among all such hyperplanes 
*	Observations lying along the margin are called support vectors
*	Once the boundary (H) has been estimated, one can apply it to training, test, or new data for forecasting. 

### Differences in SVM classifiers:
1.	How to deal with classification errors
2.	Weather the decision boundary H is a linear versus nonlinear function of the predictors 

