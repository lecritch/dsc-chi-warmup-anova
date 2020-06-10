## Imports


```python
#data manip
import pandas as pd

#stats
from scipy import stats
from statsmodels.stats.multicomp import pairwise_tukeyhsd

#viz
from matplotlib.pyplot import plot as plt

#testing
from test_scripts.test_class import Test
testing = Test()
```

## Conceptual Writing



#### Write one scenario each in which you would use a z-test, a one-sample two-tailed t-test, a two-sample one-tailed t-test, and an ANOVA


```python
'''
Your writing here

Slack your answers to Ben and he'll check 'em!
'''
```


```python
#__SOLUTION__

'''
Slack your answers to Ben and he'll check 'em!
'''
```

## Calculations

For each scenario, assume that the data come from normally-distributed populations with ~equal variances

### Question 1) 

Suppose that a random sample of n = 5 was selected from the vineyard properties for sale in Sonoma County, California,  in  each  of  three  years.    The  following  data  are  consistent  with  summary  information  on  price  per acre for disease-resistant grape vineyards in Sonoma County.  Carry out an ANOVA to determine whether there is evidence to support the claim that the mean price per acre for vineyard land in Sonoma County was not the same for each of the three years considered.  Test at the 0.05 level and at the 0.01 level.

For testing, assign your F-statistic to `f_1`, and `p_1` for the p-value


```python
data_96 = [30000, 34000, 36000, 38000, 40000]
data_97 = [30000, 35000, 37000, 38000, 40000]
data_98 = [40000, 41000, 43000, 44000, 50000]

#your code here
```


```python
#__SOLUTION__ 

f_stat = stats.f_oneway(data_96, data_97, data_98)
f_1 = f_stat.statistic
p_1 = f_stat.pvalue

print(f'f_stat {f_1}, p value {p_1}')

print('''
There is evidence to reject the null and support the hypothesis that mean value per acre 
is different at the .05 level, but not at the .01 level (though just barely.''')

#used for testing
testing.save(f_1, 'f_1')
testing.save(p_1, 'p_1')
```

    f_stat 6.834080717488789, p value 0.010440442456140328
    
    There is evidence to reject the null and support the hypothesis that mean value per acre 
    is different at the .05 level, but not at the .01 level (though just barely.



```python
#run this cell to test the f-stat

testing.run_test(f_1, 'f_1')
```


```python
#run this cell to test the p-value

testing.run_test(p_1, 'p_1')
```

### Question 2)

The  following  data  on  calcium  content  of  wheat  are  consistent  with  summary  quantities  that  appeared  in  the article  “Mineral  Contents  of  Cereal  Grains  as  Affected  by  Storage  and  Insect  Infestation”  (Journal  of  Stored Products  Research  [1992]).    Four  different  storage  times  were  considered.    Is  there  sufficient  evidence  to conclude  that  the  mean  calcium  content  is  not  the  same  for  the  four  different  storage  times?    Test  the appropriate hypotheses at the 0.05 level.

- 0 months 58.75 57.94 58.91 56.85 55.21 57.30 
- 1 month  58.87 56.43 56.51 57.67 59.75 58.48
- 2 months 59.13 60.38 58.01 59.95 59.51 60.34
- 3 months 62.32 58.76 60.03 59.36 59.61 61.95

*Hint: write a quick function to get each row of data into a list of floats after copying/pasting it down into a cell*

Store F_stat value as `f_2` and p-value as `p_2` to test!


```python
#your code here
```


```python
#__SOLUTION__

def clean_2(data_str):
    data = [float(val) for val in data_str.split(' ')]
    
    return data

month_0 = clean_2('58.75 57.94 58.91 56.85 55.21 57.30')
month_1 = clean_2('58.87 56.43 56.51 57.67 59.75 58.48')
month_2 = clean_2('59.13 60.38 58.01 59.95 59.51 60.34')
month_3 = clean_2('62.32 58.76 60.03 59.36 59.61 61.95')

f_stat = stats.f_oneway(month_0, month_1, month_2, month_3)

f_2 = f_stat.statistic
p_2 = f_stat.pvalue

print(f'f_stat {f_2}, p value {p_2}')
print('''
We have evidence to reject the null hypothesis and support the alternative hypothesis that the mean calcium content
is not the same for different storage times
''')

#used for testing
testing.save(f_2, 'f_2')
testing.save(p_2, 'p_2')
```

    f_stat 6.512085233391865, p value 0.0029819273392839582
    
    We have evidence to reject the null hypothesis and support the alternative hypothesis that the mean calcium content
    is not the same for different storage times
    



```python
#run this cell to test the f-stat

testing.run_test(f_2, 'f_2')
```


```python
#run this cell to test the p-value

testing.run_test(p_2, 'p_2')
```

### Question 3)

Use the data in the data folder to determine whether there is a difference in plant growth between a control group and two different experimental fertilizer treatments at the alpha=.05 level.

If there is a difference, determine which group had higher growth compared to which other groups 
(again at .05 alpha level).

To test your work:
- assign the F-statistic and p-value as f_3 and p_3, respectively
- assign the pvalues for any pairwise comparisons as pcp_3 

*Hint: for assigning the pairwise comparison pvalues, they are extractable from the pairwise comparison object
you create*

*read the documentation!*


```python
#your code here
```


```python
#__SOLUTION__ 

data = pd.read_csv('data/PlantGrowth.csv')

f_stat = stats.f_oneway(
    data[data['group']=='ctrl']['weight'],
    data[data['group']=='trt1']['weight'],
    data[data['group']=='trt2']['weight']
)

f_3 = f_stat.statistic
p_3 = f_stat.pvalue

print(f'''
with f_stat {f_3} and p-value {p_3}, we can reject the null that there aren"t differences in means 
between the various control and treatment groups at the alpha=.05 significance level
''')

tukey_result = pairwise_tukeyhsd(data.weight, data.group)

pcp_3 = tukey_result.pvalues
print(tukey_result.summary())
print
print("""
While there are sig. differences between the treatment groups, there aren't sig. differences b/t 
either of the treatment groups and the control group

We therefore conclude that although we can reject the null for, and found evidence that, the treatments differ from each other,
we can't reject the null that the treatments don't differ from no treatment in their effect on plant growth
""")

#used for tests
for val in zip([f_3, p_3, pcp_3], ['f_3', 'p_3', 'pcp_3']):
    testing.save(val[0], val[1])
```

    
    with f_stat 4.846087862380136 and p-value 0.0159099583256229, we can reject the null that there aren"t differences in means 
    between the various control and treatment groups at the alpha=.05 significance level
    
    Multiple Comparison of Means - Tukey HSD, FWER=0.05
    ===================================================
    group1 group2 meandiff p-adj   lower  upper  reject
    ---------------------------------------------------
      ctrl   trt1   -0.371 0.3921 -1.0621 0.3201  False
      ctrl   trt2    0.494  0.198 -0.1971 1.1851  False
      trt1   trt2    0.865  0.012  0.1739 1.5561   True
    ---------------------------------------------------
    
    While there are sig. differences between the treatment groups, there aren't sig. differences b/t 
    either of the treatment groups and the control group
    
    We therefore conclude that although we can reject the null for, and found evidence that, the treatments differ from each other,
    we can't reject the null that the treatments don't differ from no treatment in their effect on plant growth
    



```python
#run this cell to test the f-stat

testing.run_test(f_3, 'f_3')
```


```python
#run this cell to test the p-value

testing.run_test(p_3, 'p_3')
```


```python
#run this cell to test the pairwise comparison pvalues

testing.run_test(pcp_3, 'pcp_3')
```

## BONUS CONCEPTUAL QUESTION

Why are the p-values in the Tukey HSD output "adjusted"?  What does the Tukey code adjust for?

*Hint: it's the same reason we do ANOVA in the first place and not just a bunch of t-tests*


```python
'''
Your answer here

Check solution branch for answer
'''
```


```python
#__SOLUTION__

'''
The p-values are adjusted because we are making multiple statistical tests on the same data.

This is an equivalent situation to making multiple t-tests: the p-value for any given
test reflects the probability of seeing a result as or more extreme on *one* draw, *one*
roll of the dice.

But, when we make multiple comparisons, we are "rolling the dice" more than once; we 
are performing another action on the same data in the same way, and performing 
the same action that might result in our seeing results due to chance
again.

Therefore, our chosen alpha value - our specified chance of making a Type I error - no longer 
reflect the *actual chances* of making a Type 1 error. 

In order to counteract this, we *lower the alpha threshold for our chosen level of significance*
to reflect the fact that we have to look for lower p-values to get the same significance level.

Ie, instead of looking for a p-value of .05 to get 95% significance, we might look for a p-value
of .025 or .001

(the specifics depend on the number of comparisons being made)

The Tukey HSD command we run automatically adjusts the p-values to generate our chosen
level of significance (in this case, 95%)
'''
```
