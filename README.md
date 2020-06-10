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
