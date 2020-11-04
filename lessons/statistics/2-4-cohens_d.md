[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

I have run the following set of codes to compute Cohen's d for **totalwgt_lb**. <br> The calculated result was -0.0887, compared to 0.0289 for the difference in pregnancy length, so the effect is ~3x stronger. 

```
preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]

firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

def CohenEffectSize(group1, group2):
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d

CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)
```
