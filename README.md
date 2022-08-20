# Normal_Distribution

## Introduction

The normal distribution, also known as the Gaussian Distribution, is the limiting case of binomial distribution when the size of a single sample is infinitesimally small, and the number of sample in infinitely large. 

Intuitively speaking, the normal distribution is the distribution of the cumulative values generated by the random results("True"=1 or "False"=0) of infinite number of the same binomial problem.

Although the normal distribution is widely applied in natural sciences, the abundancy of its occurence has nothing to do with the physical laws, because this is in fact purely a mathematical/statistical result. 

It may resort to unchanged or quasi-static physical laws that allow mathematics to participate in nature, but the content of physical laws is irrelevant to the occurrence of the normal distribution.

For example, the heights of people follow the normal distribution. When people are growing up, their DNA, bodily condition, and the outer environment will determine whether they should continue to grow. This is somehow a random decision(people can't choose their own DNA, but of course they can choose their intake of nutrients and the outer environment, that's why people nowadays are generally taller than their previous generation), and "to continue growing or not" is somehow a "to be or not to be" question, for which the result is binomial. Their heights are the cumulative values of the decision "continue growing or not". That is why the heights of people follow the normal distribution.

The same logic applies to the IQ distribution of people. "Successfully study/train your brain or not" is a question integratedly determined by DNA, family support, world values, resources, and so on. This is somehow random among the public. The result of each training is, of course, binomial, especially when adapted to the same education system. The cumulative result of training over time is the IQ of the person, and this is why the distribution of IQ follows the normal distribution.

The same logic can be applied to the biological size of all living creatures, as well as the size of stones and so on. The size of stones also follows the normal distribution because it is the result of the random agglomeration of the particles over time.

I think the example above is enough for our understanding. To show that the arguments above really make sense, we can convince ourselves by using a simple example, as demonstrated below.

## An example to show why normal distribution is purely a statistical result.
Consider this problem: <br>
**What is the marks distribution of 1000000 students who blindly do a paper of 10000 true of false questions, with 1 mark per question?** <br>
We see that this has nothing to do with the physical laws, yet the result will follow the normal distribution, because this is a list of the cumulative values generated by random binomial results.

To justify whether the result really follow the normal distribution, we can write our code as below:<br>

First, we create a list of marks.
```
import random
list_mark = []
list1=[0,1]
student_number = 1000000
question_number = 10000
for i in range(student_number):
  mark = 0
  for j in range(question_number): 
    mark += random.choice(list1) 
  list_mark.append(mark)
```

Then, we define a function to calculate the standard deviation.
```
def variance(data, ddof=0):
  n = len(data)
  mean = sum(data) / n
  return sum( (x - mean)**2 for x in data) / (n - ddof)

def stdev(data):
  var = variance(data)
  std_dev = math.sqrt(var)
  return std_dev

sigma = stdev(list_mark)
print(sigma)
```

Finally, by using the standard deviation, we calculate the fraction of value inside range. 
```
Total_sigma1=0
Total_sigma2=0
Total_sigma3=0
Total_sigma4=0

for mark in list_mark:
  if mark >= (5000-sigma) and mark<= (5000+sigma):
    Total_sigma1+=1
  if mark >= (5000-2*sigma) and mark<= (5000+2*sigma):
    Total_sigma2+=1
  if mark >= (5000-3*sigma) and mark<= (5000+3*sigma):
    Total_sigma3+=1
  if mark >= (5000-4*sigma) and mark<= (5000+4*sigma):
    Total_sigma4+=1

Dict1 = {"μ ± σ":Total_sigma1/1000000, "μ ± 2σ":Total_sigma2/1000000, "μ ± 3σ":Total_sigma3/1000000, "μ ± 4σ":Total_sigma4/1000000}
df1 = pd.DataFrame(Dict1, index=["Expected fraction inside the range"]).T
df1
```
If the distribution of data follow the normal distribution, then we will get a result near to the Expected fraction of
population inside range(taken from [68–95–99.7 rule](https://en.wikipedia.org/wiki/68%E2%80%9395%E2%80%9399.7_rule))

|        Range        |   Expected fraction of data inside the range   |  
|        :---:        |                      :---:                     |        
| $\mu \pm 1 \sigma$  |                0.682689492137086               |       
| $\mu \pm 2 \sigma$  |                0.954499736103642               |        
| $\mu \pm 3 \sigma$  |                0.997300203936740               |
| $\mu \pm 3 \sigma$  |                0.999936657516334               |

Our result is:<br>
![image](https://user-images.githubusercontent.com/108325848/185755522-48f6df9d-bc3f-4844-a420-74bfe2f20747.png)

We can also plot the histogram the make a comparison:
```
import matplotlib.pyplot as plt

plt.figure(figsize=(8,4))
plt.hist(list_mark, bins=200, range=(4800,5200))
plt.show() 
```
The figure of the histogram of marks is:<br>
![image](https://user-images.githubusercontent.com/108325848/185757954-92e70406-7165-437f-9913-806d1e9681ba.png)

On the other hand, we can also plot the histogram of random data follow the normal distribution with the same mean and standard deviation:
```
x = np.random.normal(5000, sigma, 1000000)

plt.figure(figsize=(8,4))
plt.hist(x, bins=200, range=(4800,5200))
plt.show() 
```
The figure of the histogram of the random data generated by the normal distribution with the same mean and standard deviation is:
![image](https://user-images.githubusercontent.com/108325848/185758120-dc9e76ac-d630-434a-8246-a4eaa5f7d5b0.png)

We can see that they are very similar.
