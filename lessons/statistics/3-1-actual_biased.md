[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

actual pmf mean = 1.02   
biased pmf mean = 2.40   

```
resp = nsfg.ReadFemResp()

# Plots the actual distribution for the number of children under 18 in the respondents' households

pmf = thinkstats2.Pmf(resp.numkdhh, label='numkdhh')
thinkplot.Pmf(pmf)
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

# The below function computes the biased PMF we would get if we surveyed the children and asked them how many children under 18 are in their household.

def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf

# Plots the biased distribution for the number of children under 18 in the respondents' households

biased_pmf = BiasPmf(pmf, label='biased')
thinkplot.Pmf(biased_pmf)
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

# Plots both actual and biased distributions on the same graph

thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased_pmf])
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

# Computes the means of actual and biased distributions

pmf.Mean()
biased_pmf.Mean()
```

