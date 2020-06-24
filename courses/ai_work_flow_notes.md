
# IBM A.I. Workflow notes

## Data analysis and hypothesis testing

#### P-values
A p-value is a measure to quantify the evidence *against* the null hypothesis.
It is the probability of finding a certain result if the null hypothesis is *true*.

P-values themselves are not ground truth, they are merely a statistical tool to be used.

Modifying your data or inputs to get your p-value closer to what you desire is called, p-value hacking. Just as well this can be defined as over testing, running multiple tests on the same data.

##### Bonnferroni correction
The bonnferroni correction is a simple way to rectify the over testing issue.

$n$ = hypotheses in combined hypotheses
$$ \alpha = \frac{\alpha}{n} $$

In todays day and age when tests can scale into the hundreds and thousands this method has become less widely used in comparison to other methods.

##### Alternatives to the bonferroni correction
The statsmodels library has the following methods in the multipletests submodule.
* One step correction:
    * bonferroni
    * sidak
* Step down method using sidak adjustments
    * holm-sidak
* Step down method using bonferroni adjustments
    * holm
* Step up method (independent)
    * simes-hochberg
* Closed method based on simes tests (non-negative)
    * hommel
* Benjamin/hochberg (non-negative)
    * fdr_bh
* Benjamini/Yekutieli (negative)
    * fdr_by
* Two stage fdr correction (non-negative)
    * fdr_tsbh
    * fdr_tsbky

fbr_bh is commonly used. The p-values are ranked, multiplied by the number of features, and divided by their corresponding rank.

An example of several of the above methods:
```python
import numpy as np
from statsmodels.stats.multitest import multipletests

pvals = np.random.uniform(0.001, 0.06, 12)
_results = multipletests(pvals, alpha = 0.05, method = 'bonferroni', is_sorted = False, returnsorted = False)
rejected_bonferroni, adjusted_bonferroni = _results[0], _results[1]

_results = multipletests(pvals, alpha = 0.05, method = 'fdr_bh', is_sorted = False, returnsorted = False)
rejected_bh, adjusted_bh = _results[0], results[1]

for p, pval in enumerate(pvals):
    print(round(pval, 3), round(adjusted_bonferroni[p], 3), round(adjusted_bh[p], 3))
```

#### Posterior probability
Posterior probability is the likelihood that something will occur given relevant evidence.

It can be defined as:
$$
p(\theta|x) = \frac{p(x|\theta)}{p(x)}p(\theta)
$$

#### Bayes factor
Bayes factors is a bayesian alternative to classical hypothesis testing. Bayesian model comparison is a method of (statistical) model selection based on Bayes factors. The aim of bayes factor is to quantify the support for a model over another, regardless of whether they are correct.

It is a likelihood ratio of the marginal likelihood of two competing hypotheses, usually null or alternative.

## Machine learning, visual recognition and NLP

### Generalizing well to unseen data.
Train-test splits, cross validation and grid searching are techniques used to ensure that models are tuned in a way that they generalize well to unseen data. 

**Stratified KFold**, a variation of kfold which returns stratified kfolds, where each set contains approximately the same percentage of samples of each target class as the complete set.

**GridSearchCV** uses stratified kfold under the hood. It is very time consuming. ElasticNetCV is a possibly more effective version than the 'exhaustive version'.

### Model evaluation plots
How well a model performed can be decomposed as bias, variance and noise. 
* Bias:
  * It comes from the underlying model assumptions
  * It is the average error when the model is subjected to different training sets.
  * Associated with under-fitting, or trying to fit an inflexible model to flexible data.
* Variance:
  * A reflection of how sensitive the model is to variations in the training data.
  * Associated with over-fitting.
Possible solutions:
* Bias:
  * Add more features, with additional data or feature engineering
  * A more sophisticated model
  * Decrease regularization
* Variance:
  * Fewer features: techniques such as variance thresholding, ANOVA, manifold learning and matrix decomposition.
  * A simpler model.
  * More training samples.
  * Increase regularization.

### Relating the evaluation metric to a business metric
A business metric is a quantifiable event that is directly used to measure the success or failure of a business opportunity.

### Regularized regression
**Regularization** is a technique to control over-fitting by introducing a penalty term.

## Machine learning, visual recognition and nlp

### Bagging and random forest
Bootstrapping can be a useful way to help make estimate. In Sci-kit learn you create a BaggingClassifier, as a wrapper for a model, like an SVM. In a very similar manner to grid searching.

### Boosting, ensemble model
Boosting is essentially taking several weak learners (models only slightly better than random chance) and creates a single strong learner. Boosting builds its ensemble sequentially, unlike random forest which do so in parallel.

### Ensemble learning
Ensemble learning through model averaging, Bayesian model averaging, model stacking, majority vote and other methods are among the best performing methods known in machine learning.

### Neural networks: Through the eyes of our working examples
When choosing a model for deployment a neural network is often a great and powerful choice, but it comes with the cost of complexity and often, computation time and needs. If you were to have two models that perform similarly then you should default to the simpler model. In the long term the maintenance required for a neural network is much greater than that of a simpler model.

Neural networks can be seen as non-linear function approximators.

## Enterprise model deployment
Make it work, make it better, make it faster.

## The design process
When going through the design process remember to, observe, reflect and make. This means making fast changes to the model in response to user feedback.

### Docker
A docker container is a running process that is kept isolated from the host and from other containers. One of the important consequences of this isolation is that each container interacts with its own private filesystem. A docker image includes everything needed to run an application: code, runtime libraries, and a private filesystem.

Before moving to a high performance computing environment, try optimizing your model with tools like apache spark.