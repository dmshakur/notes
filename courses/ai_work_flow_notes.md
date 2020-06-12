
# IBM A.I. Workflow notes

## Data analysis and hypothesis testing

### Week 2

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

#### Posterier probability
Posterior probability is the likelihood that something will occur given relevant evidence.

It can be defined as:
$$
p(\theta|x) = \frac{p(x|\theta)}{p(x)}p(\theta)
$$

#### Bayes factor
Bayes factors is a bayesian alternative to classical hypothesis testing. Bayesian model comparison is a method of (statistical) model selection based on Bayes factors. The aim of bayes factor is to quantify the support for a model over another, regardless of whether they are correct.

It is a likelihood ratio of the marginal likelihood of two competing hypotheses, usually null or alternative.

