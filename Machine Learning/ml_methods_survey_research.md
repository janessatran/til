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
<img src="https://s3.amazonaws.com/production.scholastica/attachment/9153/large/merged_scatter_plots.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAI7SMXV4JOVMX437Q%2F20181210%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20181210T162027Z&X-Amz-Expires=10000&X-Amz-SignedHeaders=host&X-Amz-Signature=6d193dd46876004749f1221711d20c573e1eb4563385442c1646ccfee7e337a2">


### Differences in SVM classifiers:
1.	How to deal with classification errors
2.	Weather the decision boundary H is a linear versus nonlinear function of the predictors 

* most often, the decision boundary is nonlinear
 * can use a **soft margin** classifier, which allows for 
  1. observations that are correctly classified but lie between M and H
  2. misclassified observations
 * soft margin classfiers use slack variables which keep track of the margin error for each observation
 * to find the optimal boundary H for soft margin classifiers, we need to maximize the margin while also specifiying a constraint on total error T that will be allowed 
  * for optimization, can also use penalty C
  * large penalties C (small allowances T), lead to smaller margins
  * smaller penalties C (large allowances T), lead to larger margins, but also more misclassfications in the training data 
  * penalty C / allowance T usually set through k-fold cross-validation 

### SVM Advantages and Disadvantages
|  Advantages 	|  Disadvantages 	|
|---	|---	|
| Robust to obserations that are far away from hyperplane and are efficient since they are based only on support vectors within hyperplane.   	|  Copmutationally intensive and require large amount of memory to perform estimation, especially if data sets are large. 	|
|Perform well even when there are a large number of predictors and a small number of cases in the dataset.   	| For nonlinear applications, user must select kernel to be used by the SVM. Choice of kernel and any associate hyperparameters is essential- incorrect choice can negiatively affect performance.  	|
| SVMs can adapt to nonlinear decision/classification boundaries.  	|  SVMs can seem like black boxes in that a final funcitonal form or table of coefficients for various predictors is not provided as part of estimation. 	|
| Because they are constructed using only the support vectors, they may ave better classfication performance when applied to data that are unbalanced with respect to the binary outcome.  	|   	|

## Using LASSO to Model Interactions and Nonlinearities in Survey Data
source: [https://www.surveypractice.org/article/2716-using-lasso-to-model-interactions-and-nonlinearities-in-survey-data](https://www.surveypractice.org/article/2716-using-lasso-to-model-interactions-and-nonlinearities-in-survey-data)
* **LASSO**: Least Absolute Shrinkage and Selection Operator
* Applies shrinkage factors to regression coefficients to perform **feature selection** and optimze the form of regression model more efficientily
* Good for "sparse data" situations (many predictors available, but only a few are assumed ot be related to dependent variable) 
 * e.g. Using census block group data + address-based samples to predict likelihood of survey response
* Can be used for both categorical and continuous data with a mix of predictor types
* LASSO shrinks the magnitude of cofficients to zero (to eliminate regressors)- nonzero coefficients are estimated for true predictors, zero coefficients are deemed irrelevant 

Summary: Lasso regression analysis is a shrinkage and variable selection method for linear regression models. The goal of lasso regression is to obtain the subset of predictors that minimizes prediction error for a quantitative response variable. The lasso does this by imposing a constraint on the model parameters that causes regression coefficients for some variables to shrink toward zero. Variables with a regression coefficient equal to zero after the shrinkage process are excluded from the model. Variables with non-zero regression coefficients variables are most strongly associated with the response variable. Explanatory variables can be either quantitative, categorical or both.

### LASSO Advantages and Disadvantages
| Advantages  	|  Disadvantages 	|
|---	|---	|
| Implicit variable selection from coefficient shrinkage; good for sparse data scenarios  	|  Does not provide estimates of uncertainty when run once; to obtain measures of uncertaintiy, need to bootstrap or estimate a Bayesian LASSO. 	|
| Unlike stepwise regression models that include or exclude a variable or variables at each step, LASSO-based methods estimate a single model.  	|  In some situations, LASSO may not be consistent. Need ALASSO for consistency. 	|
| ALASSO models have "oracle property" combining consistency and efficiency  	| LASSO-based methods have difficulty differentiating relevant and irrelevant predictors when predictors themselves are highly correlated.  	|
|   	| Under certain basis expansions, LASSO-based model can be computationally intensive and require more time than traditional approaches.  	|
