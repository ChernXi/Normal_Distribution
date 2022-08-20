# Normal_Distribution

## Introduction

The normal distribution, also known as the Gaussian Distribution, is the limiting case of binomial distribution when the size of a single sample is infinitesimally small, and the number of sample in infinitely large. 

Although normal distribution is widely applied in natural sciences, but the abundancy of its occurence has nothing to do with the physical laws, because this is in fact purely a mathematical/statistical result. 

Yes, unchanged(or at least quasi-static) physical laws allow mathematics to take part in nature, but other than that, the content of physical laws is irrelevant to the occurence of the normal distribution.

For example, the heights of people follow the normal distribution. When people are growing up, their DNA, bodily condition, and the outer environment will determine whether they should continue to grow. This is somehow a random decision(people can't choose their own DNA, but of course they can choose their intake of nutrients and the outer environment, that's why people nowadays are generally taller than their previous generation), and "to continue growing or not" is somehow a "to be or not to be" question, for which the result is binomial. Their heights are the cumulative values of the decision to "continue growing or not". That is why the heights of people follow the normal distribution.

The same logic applies to the IQ distribution of people. "Successfully study/train your brain or not" is a question integratedly determined by DNA, family support, world values, resources, and so on. This is somehow random among the public. The result of each training is, of course, binomial, especially when adapted to the same education system. The cumulative result of training over time is the IQ of the person, and this is why the distribution of IQ follows the normal distribution.

The same logic can be applied to the biological size of all living creatures, as well as the size of stones and so on. The size of stones also follows the normal distribution because it is the result of the random agglomeration of the particles over time.

I think the example above is enough for our understanding. To show that the arguments above really make sense, we can convince ourselves by using a simple example, as demonstrated below.

## An example to show why normal distribution is purely a distribution of the cumulative values of random binomial constant.
Consider this problem: <br>
**What is the marks distribution of 500000 students who blindly do a paper of 5000 true of false questions, with 1 mark per question?** <br>
We see that this has nothing to do with the physical laws, yet the result will follow the normal distribution, because this is a list of the cumulative values generated by random binomial results.

To do this justify whether this really follow the normal distribution, we can write our code as below:<br>
First, we create a list of marks.
```
import numpy as np
import random
list_mark = []
list1=[0,1]
student_number = 500000
question_number = 5000
for i in range(student_number):
  mark = 0
  for j in range(question_number): 
    mark += random.choice(list1) 
  list_mark.append(mark)
```

