
## IST 718 - Random Forest 

### Scribers -  Rohan Nitin Mahajan, Jan Lennart Zeugner.


### Problem: Credit Score

- Predict whether someone will be in financial distress or not.


#### A problem with Logistic regression:
- While logistic regression is a good tool for classification problem it also comes with certain limitations 
- Since logistic regression is a linear model, the boundaries between classes are also going to be linear

<center><img src="IST 718 image10.PNG" width="50%" align="center"></center>

<center>$$p(y| x_1, x_2,\theta_1, \theta_2, \theta_3) = \sigma(E\theta_ix_i)^{y} ({1 - \sigma(E\theta_ix_i)^{1-y})}$$
<br>
<center>$$\sigma(z) = \frac{1}{1 + e^{-z}}$$
    <br>
<center>
$$p(y =1| x_1, x_2,\theta_1, \theta_2, \theta_3) = \sigma(E\theta_ix_i)^{y} = \frac{1}{1+e^{E\theta_ix_i}} > \alpha $$
<br>
<center>$$\frac{1}{1+e^z} > \alpha  = \frac{1}{\alpha} > 1 + e^{-z} $$
<br>
<center>
$$\frac{1}{\alpha} - 1> e^{-z}$$
<br>
<center>
$$ \log \frac{1-\alpha}{\alpha} > -z$$
<br>
<center>
$$ \log \frac{1-\alpha}{\alpha} >-\theta_1, -\theta_2, -\theta_3$$
<br>
<center>
$$ x_2 > \frac{\log \frac{1-\alpha}{\alpha}-\theta_0}{\theta_2} - \frac{\theta_1 x_1}{\theta_2}$$ 
<br>
<center>$$ x_2> a+bx_1$$
    

    
    
    





## Decision Trees:

- Classification method
- Each node contain a condition/question.
- Answers to the questions - Path that leads to another node.
- Decision tree recursively partitions the feature space into regions R.


#### Prediction:
- For regression:
     - predict the average of a region and evaluate on squared error: 




$$\sum_{m=1}^{M}\sum_{i \in R_m} {\left(y_i - \hat y_{R_m}\right)^2}$$


- For classification:
    - predict the majority of a region and evaluate on distribution of predictions:  

<center> **Gini index** $\qquad\; G_m = \sum_{k=1}^{K} {\hat p_{mk}(1 - \hat p_{mk}})$  
<center> 
  **Cross entropy** $\quad D_m = - \sum_{k=1}^{K} {\hat p_{mk}\log(\hat p_{mk}})$

## Optimization of Decision Trees:
- Proposes candidate splits.
- When splitting the data into regions, we attempt to create regions with following a uniform distribution.

<center><img src="IST 718 image11.PNG" width="50%" align="center"></center>

- The more regions, there are the better th loss
- However, the more regions, the more likely we are to overfit
- Therefore, we need to prune trees to prevent overfitting.
- Use regularization to penalize leafes

### Problems with Decision Trees:
- There are too many ways to fit the data and, therefore, decision trees tend to overfit and result in too much variance.

## Pros and Cons of Decision Trees:

#### Pros:
- Easy to explain and interpret
- Can easily be visualized
- Limited feature engineering required as trees can handle qualitative variables

#### Cons:
- Low predictive accuracy 
- Not very robust



##### One major problem with Decision Trees is that they have a very high variance.
- However, we can create multiple decision trees and average the results of them.

### Example - Height of Person
- Take average opinion of people to derive a person's height.



<center><img src="IST 718 image6.PNG" width="50%" align="center"></center>

- Following central limit theorem (CLT) and given a gaussian distribution, sample variance is smaller than population variance


## Bagging:
- Simulate training datasets. 
- Bootstrapping training data
    - sample with replacement

<center><img src="IST 718 image7.PNG" width="50%" align="center"></center>

### Prediction with Bagging
- use several trees and average the predictions of each decision tree and, thus, reduce variance


<center>
<br>
  **Regression** $\qquad \hat{f}_{\text{bagging}}(X) = \frac{1}{B}\sum_{b=1}^{B}{\hat{f}^{*b}(X)}$  
<br>
  **Classification** $\quad \hat{f}_{\text{bagging}}(X) = \text{majority}\{\hat{f}^{*b}(X) \mid b \in \{1, \ldots , B\}\}$  

### Limitations of bagging:  
- Since we are resampling, data points will be reused and trees become correlated. 
- Correlation affects the outcome as it creates bias

$$var(f) = \left(\frac{1 - \rho}{B} + \rho \right) \sigma^2$$  

<center><img src="IST 718 image8.PNG" width="50%" align="center"></center>

### Tree Bagging & Free Validation/Test Data
- Why do we get a free validation/test data?

<center><img src="IST 718 image9.PNG" width="50%" align="center"></center>

$$\sum_{m=1}^{M}\sum_{i \in R_m} {\left(y_i - \hat y_{R_m}\right)^2}$$

- When drawing from a sample the probability of being selected is:   $p(s_{sad})$ = $\frac{1}{n}$ 
- The probability of not being selected and being the sad sample is: $p(s_{sad}^C)$ = $1 - \frac{1}{n}$
- The probability of not being selected twice follows: $p(s_{sad}^C)$ = $1 - \frac{1}{n}^2$
- The probability of not being selected at all with sample size n follows: $p(s_{sad}^C)$ = $1 - \frac{1}{n}^n$
- We can calulate the limit of: $ e = \lim_{n \to \infty} (1+\frac{1}{n})^n$
<center>
$ e^a = \lim_{n \to \infty} (1+\frac{a}{n})^n$
<center>
$ e^a = \lim_{n \to \infty} (1+\frac{1}{n})^n = e^{-1} = \frac{1}{e} = 0.33$
    
    

