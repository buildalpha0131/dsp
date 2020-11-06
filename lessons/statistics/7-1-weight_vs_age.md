[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

The scatterplot shows a weak relationship between the variables.      

Pearson's correlation is ~0.07, and Spearman's is ~0.09, so the difference between them suggests some influence of outliers or a non-linear relationship.     

Plotting percentiles of weight versus age suggests that the relationship is non-lionear, with birth weight increasing more quickly in the younger age range.     

```
import numpy as np

import brfss

import thinkstats2
import thinkplot

import first

live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])

ages = live.agepreg
weights = live.totalwgt_lb

thinkplot.Scatter(ages, weights, alpha=0.1, s=10)
thinkplot.Config(xlabel='Age (years)',
                 ylabel='Birth weight (lb)',
                 axis=[10, 45, 0, 15],
                 legend=False)
                 
def BinnedPercentiles(df):
    """Bin the data by age and plot percentiles of weight for each bin.

    df: DataFrame
    """
    bins = np.arange(10, 48, 3)
    indices = np.digitize(df.agepreg, bins)
    groups = df.groupby(indices)

    ages = [group.agepreg.mean() for i, group in groups][1:-1]
    cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups][1:-1]

    thinkplot.PrePlot(3)
    for percent in [75, 50, 25]:
        weights = [cdf.Percentile(percent) for cdf in cdfs]
        label = '%dth' % percent
        thinkplot.Plot(ages, weights, label=label)

    thinkplot.Config(xlabel="Mother's age (years)",
                     ylabel='Birth weight (lbs)',
                     xlim=[14, 45], legend=True)
    
BinnedPercentiles(live)

print('Corr', Corr(ages, weights))
print('SpearmanCorr', SpearmanCorr(ages, weights))
```
