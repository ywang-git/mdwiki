
# Machine Learning Bootcamp
a *feature* is an individual measurable property of a phenomenon being observed

## objective
### basic terminology
- observations
- target variables
- supervised learning
- classification
- regression
- loss functions
- inference

### build models correctly
- collect data
- build a model
- evaluate model performance
- deploy the model in production

### tools / resources

## Basic technique
- simple classification
- regression
- clustering
## Advanced technique
- multi-class classification
- semi-supervised learning
- latent factor models
- sequential models


Classification: discrete result
Regression: continuous result

## Concepts Overview

### what is ML?
predict ->
new data based on observed data
extract -> 
hidden structure from the data
summarize ->
data to concise descriptions
optimize ->
an action given a cost function and observed data
 adapt
 based on observed data
### why learn?
when you cannot code it
cannot scale
need to adapt
cannot track

### key concepts
- supervised learning
- loss functions
- overfitting
- underfitting
- bias-variance trade-off
### supervised learning
two phases
1. training
2. prediction

#### classification (categorical)
model F: logistic regression, decision trees, random forests, support vector machines, naive bayes

#### regression (ordinal / real-valued)
model F: linear regression, regression trees, kernel regression

###Loss Functions
difference between the trained result and the real result
goal: to find model f where loss function $L$ is minimum

\\[F^{*} = arg_{F} min[ \sum_{i \in D}L(Y_i, F(X_i)) ]\\]
$L(Y, F(X))$

- squared loss $(Y-F(X))^{2}$ (both linear regression and classification problems)
- logistic loss $log(1 + e^{-YF(X)}) (Y \in \{+1, -1\})$ (logistic regression, only classification problems)
- hinge loss $max(0, 1 - Y \cdot F(Xi)) (Y \in \{+1, -1\})$ (support vector machines, only classification problems)

### overfitting
predict data on training data well, but predict unseen data poorly
reason: there are noisy patterns in the training data captured by the model

### underfitting
lacks expressive power to capture target distribution (poor training)

### bias-variance tradeoff
bias: difference between average model prediction and true target value (underfit)
variance: variation in predictions across different training data samples (overfit)

| \\ | low variance | high variance |
| ---- | ---- | ---- |
| **low bias** |  | complex models with large # parameters <br /> e.g. linear models with many sparse features, decision trees <br /> reduce variance by increasing training data and decreasing model complexity (feature selection, aggressive regularization parameter) |
| **high bias** | simple models with small # parameters <br /> e.g. linear models with few features <br /> reduce bias by increasing model complexity (adding more features, decreasing regularization) | |

## linear models
$F(X) = W \cdot X$ W is a vector of feature weights

#### training
learning weights that minimize loss $\sum_{i \in D} L(Y_i, W \cdot X_i))$

#### prediction
- regression: $Y = W \cdot X$
- classification: threshold

Learning algorithms

#### batch learning
- gradient descent: each iteration update weights by gradient of overall loss function
   $ W = W - \eta \cdot \frac { dL} {dW}$ ($\eta$ is learning parameter)
- BFGS and L-BFGS: each iteration, update weights by product of (approximate) inverse of Hessian H and gradient of the overall loss function
   $ W = W - H^{(-1)} \cdot \frac{dL}{dW}$
H: matrix of the second order derivatives of the loss function

#### online learning
each update looks at a single instance
- Stochastic Gradient Descent (SGD): in each iteration, update weights by gradient of local loss function (scale) $L_{i} = L(Y_i, W \cdot X_i)$
  $ W = W - \eta \cdot \frac {dL_i} {dW}$
 
### regularization
 prevent overfitting in linear models; by penalizing large weight values
- L1 regularization
Add a term $\lambda_1 \cdot ||W||_1$ to loss function $L$: aggressively reduces number of non-zero weights
- L2 regularization
Add a term $\lambda_2 \cdot ||W||_2$ to loss function $L$: less aggressive in forcing weight values to zero

## decision trees and random forests
leaf nodes associated with class label / numeric values

### Learning (Tree induction)
split nodes top-down using greedy strategy
to split node, select attribute-value pair $(X_i, v)$ that maximize purity
- purity criteria: entropy, gini-index, variance
- push training examples into child nodes ($X_i < v$->left, $X_i > v$ -> right)

### prediction
follow path from root to leaf such that new example X satisfies split conditions along path
- classification: majority class label in leaf
- regression: mean label value in leaf

### random forest - ensemble of decision trees

bootstrap: induces diversity
construct decision trees considering a random subset of attributes for each node split (reduces correlation)


## k-nn prediction (K-nearest neighbor prediction)
key: predict label for a new instance $X$ based on target values $Y$ of $K$ nearest neighbors of $X$
neighbors are determined based on an appropriate distance metric (e.g. Euclidean distance)

## neural networks

key: multiple layers including hidden ones to capture complex non-linear dependencies between input variables $X$ and target $Y$

## bayesian learning
key: assume a probabilistic generative model for $(X, Y)$, estimate the joint model parameters & infer target class probabilities $p(Y|X)$
- each instance $X_i$ comprises multiple features $[X_{i1}, \cdots X_{im}]$
- generative model: feature $X_{ij}$'s are conditionally independent given target class $Y_i$

\\[p(Xi, Yi) = p(Yi) \cdot p(X_i | Y_i) = p(Y_i) \cdot \prod_j p(X_{ij}|Y_i)\\]

- class probabilities can be estimated via Bayes rule and used to find most likely label

\\[p(Y_i | X_i)  \propto p(Y_i) \cdot \prod_j p(X_{ij} | Y_i)\\]

## unsupervised learning
no target variable
goal: capture the hidden structure / patterns in the data
(clustering / matrix factorization (PCA, SVD) / topic models (LDA, PLSA), other probabilistic latent factor models / association rule mining)

- k-means clustering
partition data instance into $K$ disjoint groups

problem: given data instances $\{X_1, \cdots , X_n\}$, find cluster assignment (partitioning) $h: \{1, \cdots n\} \rightarrow \{1, \cdots , K\} $ & cluster representatives $M = \{ \mu_1, \cdots , \mu_k\}$ to minimize total "distance" between each instance & its cluster representative
\\\[\arg_{h, M}\min \sum_i \Vert   X_i - \mu_{h(i)} \Vert  ^2\\\]

algorithm:
- randomly initialize cluster representatives $M = \{ \mu_1, \cdots , \mu_k\}$
- repeat until convergence
  - [optimize h] assign each $X_i$ to cluster $j$ so that $\Vert X_i - \mu_j \Vert^2$ is minimum
  - [optimize M] Re-compute representative $\mu_j = \frac{\sum_{h(i) = j}X_i}{\sum_{h(i) = j}1}$ for each cluster $j$

## Comparison
| \\ | Pros | Cons |
| ---- | ---- | ---- |
| Decision Trees | <li> extremely fast at classifying new instances <li> easy to interpret for small-sized trees <li> can capture complex non-linear behavior using conjunctions over attributes (feature engineering effort is minimal) | <li> decision boundaries are rectilinear <li> high variance, i.e., small variations in the data can generate very different trees <li> very susceptible to overfitting, i.e., large trees learn patterns in noice -> training error keeps going down, but test error goes up  |
| $K$-Nearest Neighbor Methods | learning is very simple, can learn complex target functions | need to store every training example; prediction is slow; predictions often sensitive to choice of $K$|
| neural networks | can learn non-linear functions | not easily interpretable, complex multi-layer learning algorithms (e.g. back-propagation), slow to converge |
| Naive Bayes Classifier | learning is straightforward | class-conditional independence does not always hold, smoothing is required for sparse features |

#Module 1: Classification

## Problem Definition

### Key Elements
- Observation: a data object, a single entity of the data the learning process is operating on
- Feature: part of the data in the observation that the learning process cares about (*attributes* or *variables*)
- Label: the target variables, which is the result of the predication (and verification during training), required by supervised training

###  Defining the Problem


## best scenarios
1. enough data
2. pattern discovery with little mistakes (underfit)
3. generalized pattern (overfit)

## Read Data
```python
>>> import pandas as pd
>>> train_data = pd.read_csv('adult.text', header=None, skiprows=[0], error_bad_lines=False, compression=False)
```

## Preprocess Data (preparation and cleaning)
1. add header (`data.columns = []`)
2. drop unnecessary column (`data.drop('...', axis=1)`)
3. specifying data types
4. type conversion
  - categorical and binary variables to Str (`data[...] = data[...].astype(np.str)`)
  - numeric variables to Float (`data[...] = data[...].astype(np.float)`)
5. removing whitespaces (`data[...] = data[...].map(lambda x : x.strip())`)
6. binarizing class labels
7. impute missing values (`data[...].fillna(value=..., inplace=True), mode()`)
8. randomly shuffle training data (`data = data.sample(frac = 1)`)

other steps:

- outliers
  genuine or erroneous?? (decision trees more resilience??) 
  remove / change value using strategy for missing data
- feature scaling
  $f_i = \frac{f_i - mean}{standard deviation}$
  faster to converge
- downsampling
  stratified sampling (to reduce sample size)
  in the case with skewed occurrence of one class (minor class might be ignored): downsample the dominant class, creating a new training dataset retaining all examples belonging to the minority class and a sample containing an equal number of examples from the majority class 
- importance weight
  - instead of downsampling the majority class, assign an importance weight to each example from the minority class (ratio of the majority and minority classes)
  - application need (penalizing misclassification)

## Data visualization and analysis

### Overview

- [seaborn]( http://stanford.edu/~mwaskom/software/seaborn/)
- [Matplotlib](http://matplotlib.org)

### Feature and Target Summaries

detect outliers and skew in the feature or target data distribution

#### Summary Reports
```python
import seaborn as sns
import matplotlib.pypolot as plt

%matplotlib inline
```

``` python
data.describe()
```

``` python
for var in categorical_variables:
	print("histogram for " + var)
	print(data[var].value_counts())
```

#### Histograms

``` python
sns.displot(data.age, bins = 25, kde = False)
plt.title('Histogram of Age')
plt.xlabel('Age')
plt.ylabel('Count')
```

### Feature - Target Correlations

- keep features with high correlation (signal)
- filter out the features with low correlation (noisy)

``` python
sns.distplot(train_data[train_data['class'] == '0'].age, bins = 25, kde = False, label = "< $50k")
sns.distplot(train_data[train_data['class'] == '1'].age, bins = 25, kde = False, label = ">= $50k")
```

what happens without `bins` specified?

### Feature - Feature Correlations
- which feature is redundant, if two features are highly correlated, maybe only keep one

*scatter plots*: difficult to visualize
*[smoother](https://en.wikipedia.org/wiki/Scatterplot_smoothing)*: fit a curve to the data points to uncover functional relationship between variables

```python
sns.set(color_codes=True)
train_data['education-num'] = train_data['education-num'].map(int)
sns.regplot('education-num', 'hours-per-week', train_data[train_data['class'] == '0'], 
            scatter_kws={"marker": ".", "color": "red"},
            line_kws = {"linewidth": "1", "color": "red"},
            order = 3,
            label = ' <= $50k')
sns.regplot('education-num', 'hours-per-week', train_data[train_data['class'] == '1'], 
            scatter_kws={"marker": ".", "color": "green"},
            line_kws = {"linewidth": "1", "color": "green"},
            order = 3,
            label = ' > $50k')
plt.xlabel('Number of years of education')
plt.ylabel('Hours per week')
plt.legend(loc="lower right")
plt.title("Scatter plot of hours worked per week and number of years of education")
```
### Interpret Scatter Plot

## Feature Engineering


### Overview

put visual intuitions into actionable features

*feature engineering*: manipulating raw data into new more useful representations, most critical and time-consuming step of predictive model building, requires lots of trial and error combined with domain knowledge and ingenuity

### Feature Engineering Overview

improve the expressive power of linear models: introduce non-linearity through feature transformations

- non-linear data transformation: includes transformations such as numeric attribute binning and combinations of existing features
- domain-specific features: includes text features, features that capture the structure of a web page and specialized features (e.g. SIFT) for image data
- data-driven features: e.g. meta features derived from clusters with the data
- feature selection: selecting a subset of relevant features from a much larger set, eliminate noisy features or to make model learning computationally feasible (optimization)

*numeric feature binning* and *quadratic features*: only for linear models (not decision trees or random forests)

### Numeric Feature Binning

1. partition the domain of a numeric attribute into contiguous and treat each binds as a separate feature
2. the feature for a numeric attribute is simply the bin that the numeric attribute value belongs to

improves the quality of an ML model by not "distracting" the learning process with precise numeric values when input precision exceeds that of the desired output

make the continuous value discrete ~~break one feature into different features~~ create a new feature that is categorical based on the numeric value

optimum number of bins: depending on attribute characteristic, determined by experimenting

### Quadratic Features

combine paris of existing features (generalization: combine any number of features - *cartesian product* between features)
group base features and define new quadratic features comprising pairs of base features from the different groups

#### Example
create quadratic feature / cartesian product of feature when we believe there is a correlation between the combination of a group of features and the target

The quadratic pairing between a categorical and a numeric feature happens in two phases: 
1. the numeric feature is transformed into a categorical feature using binning
2. the pairing is performed between the two categorical features

### Additional Notes

* including feature: more features -> improve prediction accuracy 
* feature selection: reduce noise, use important score returned by ML algorithms
* Numeric Feature
  * supervised numeric binning algorithms
	  select binning strategy by taking into account class labels: 
	  * information gain (classification)
	  * variance reduction (regression)
  * fixed depth decision tree
	  multidimensional extension, using a fixed depth decision tree; each leaf index as a separate binary feature
* quadratic feature
  Example: combine features in text (sequence of tokens), such as book title and binding to decide whether a book is a text book

## Model Training and Parameter Tuning

### Model Training

training phase: identifying a model that maximize its performance (minimizes its loss) in the context of the training data

### Model Parameter Tuning

### Additional Notes:

**loss function**

**Stochastic Gradient Descent**

**overall learning rate**: the gradient in each weight update of SGD is multiplied by an overall learning rate that is decayed (initial fast approach to desired weight, reduce the magnitude of change after a while)

**adaptive learning rate**: OLR is decayed individually for each feature proportional to the square root of the sum of squares of gradients at past examples (large past gradients had large updates already, limit the learning rate to dampen the magnitude of the subsequent updates)

**L1/L2 regularization**

**Feature Hashing**: to handle a large number of features, hashes features and then learns weights for the hashed feature?? (dimensionality reduction technique, randomly projects disjoint subsets of features onto different has values)

## Model Evaluation

### Overview

#### Constructing Fair Evaluations

real-world data from same distribution

- 70-80% training data
- 20-30% testing data

### Classification Evaluation Metrics
#### Making Predictions Using a Classification Threshold
**prediction score** - output of many binary classifier systems, indicating system's certainty that the given observation belongs to the positive class (may be scaled to fixed interval)

to make decision: pick a threshold

different requirements:

- high precision: tolerant on mistaking positive as negative 
- high recall: tolerant on mistaking negative as positive

#### Prediction Accuracy as an Evaluation Metric

the number of correct answers as a fraction of the total number of predictions

two problems:

- highly unbalanced dataset
- cost of getting a false positive and false negative are not equal

#### Precision and Recall

confusion matrix

| \\ | True Value: 1 | True Value: 0 |
| ---- | ---- | ---- |
| **Prediction: 1** | True Positive (TP) | False Positive (FP) |
| **Prediction: 0** | False Negative (FN) | True Negative (TN) |


1. `Precision = P(observation is positive | classifier labels as positive)`
2. `Recall = P(classifier labels as positive |  observation is positive)`

#### True Positive and False Positive Rates

**Receiver Operating Characteristic (ROC)**

* **True Positive Rate** (TPR, i.e. recall or sensitivity): `TP / (TP + FN)`
*  **False Positive Rate** (FPR, i.e. one minus specificity): `FP / (FP + TN)`

#### Evaluating Binary Classifiers with ROC Curves

ROC graph: plotted by "sweeping" through the range of all possible thresholds (within some reasonable bounds on precision). For each threshold, the TPR and FPR are calculated, and the results are plotted on a graph, where y asix is **TPR**, and the x axis is **FPR**.

* **The perfect curve**: the curve hugging the upper-left corner, corresponding to high TPR and low FPR across the range of the thresholds.  (indication of no hard threshold decision)
* **Diagonal Line**: worst case scenario. The classifier is unable to make a distinction between precision and recall.
* **Turning a bad classifier into a good classifier**: curve that hugs the lower-right corner. flip the sign
* **Area Under Curve** (AUC): the closer to 1, the larger the difference between 0.5, the better.

### Further Performance Evaluation Analysis in Python

```python
import sklearn.metrics
import pandas as pd
import matplotlib.pyplot as plt
 
%matplotlib inline
 
def plotRoc(fpr, tpr, auc):
  plt.figure()
  plt.plot(fpr, tpr, label='ROC curve (AUC = %0.2f)' % auc)
  plt.plot([0, 1], [0, 1], 'k--')
  plt.xlim([0.0, 1.0])
  plt.ylim([0.0, 1.0])
  plt.xlabel('False Positive Rate')
  plt.ylabel('True Positive Rate')
  plt.title('Receiver operating characteristic example')
  plt.legend(loc="lower right")
  plt.show()
 
def plotMetrics(score_file_name):    
  df = pd.read_csv(score_file_name)
  y_true = df['trueLabel']
  y_score = df['score']
  auc = sklearn.metrics.roc_auc_score(y_true, y_score)
  fpr, tpr, thresholds = sklearn.metrics.roc_curve(y_true, y_score)
  plotRoc(fpr, tpr, auc)
 
PREDICTION_FILE_NAME = 'prediction'
plotMetrics(PREDICTION_FILE_NAME)
```

### Additional Notes

#### K-fold Cross-Validation

technique for generating test data to calculate model performance metrics and find the optimal settings for learning algorithm parameters

1. randomly split training set into K parts
2. $K$ training-test splits are created, each training set containing $K-1$ parts and the test set containing the remaining part
3. for each training-test split, a predictive model is trained against the training set and the model's performance is then evaluated on the test set
4. final model performance score is the average of the $K$ model performance scores

typical $K$ is between 3 and 5

#### Troubleshooting Model Performance

high bias / underfitting (increase model complexity):

* increase the number of features (e.g. more feature combinations, increasing n-grams size, increase number of numeric attribute bins)
* decrease the regularization parameter values

high variance / overfitting (decrease model complexity):
* increase the number of training examples
* decrease the number of features (e.g. feature selection, fewer feature combinations, decreasing n-grams size, decreasing number of numeric attribute bins)
* increase regularization parameter values

## Model Deployment
### Overview
#### Types of Predictions
* Bulk prediction: no low latency, upload -> create predication -> download
* Online prediction: low latency
* Local prediction: extremely latency sensitive

#### Model Retraining
monitor deviation, trigger retrain

# Module 2: Regression

## Data Preparation and Cleaning

```python
>>> data = data.rename(columns = {'MarketPlace Id':'marketplace_id'})
```

> Written with [StackEdit](https://stackedit.io/).