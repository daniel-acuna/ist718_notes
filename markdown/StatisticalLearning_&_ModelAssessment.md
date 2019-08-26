# Advanced Statistical Learning and Model Assessment #
## Scribe: Adam Miller ##
## February 19, 2019 ##

## Part 1: Advanced Statistical Learning ##
### Logistic Regression ###
  - The method for maximizing the likelihood for logistic regression is similar to that for Gaussian, 
  except that the *negative log-likelihood* is expressed and then *minimized*
  - Find the nLL by performing a gradient descent:
  <p align = "center">
  <img src = "https://github.com/adamiller/ist718_notes/blob/master/markdown/image/gradient%20descent.PNG" width = 40%>
  </p>
  
  - Derivation:
   <p align = "center">
   <img src = "https://github.com/adamiller/ist718_notes/blob/master/markdown/image/gradient%20descent%20derivation.PNG" width = 40%>
   </p>
   - The first theta term after the sigma represents how wrong the prediction is

### Accuracy vs. Interpretability ###
  - Simple models are less accurate but more interpretable, and complex models vice-versa:
  <p align = "center">
  <img src = "https://github.com/adamiller/ist718_notes/blob/master/markdown/image/interpretability_vs_acc.PNG" width = 50%>
  </p>
  
### Unsupervised vs. Supervised Learning ###
  - Supervised: each X has an associated Y
    - Easier because there is always an evaluation available for the model
  - Unsupervised: each X has no known association, or no "ground truth"
    - In general more difficult because there is no clear way to evaluate the model
    - Examples: Clustering, topic modeling, dimensionality reduction

### Major Takewaways ###
  - Statistical learning acknowledges uncertainty and tries to learn a stochastic model of the data.
  - We need to define a model of the data.
  - We need to estimate the parameters of such model.
  - We can use that model to predict or interpret the results.
  - We can use supervised learning to learn a relationship between variables.
  - If variables are not quantitative, we use classification models.
  
## Part 2: Model Assessment ##
### Generalization Performance ###
- Define a loss function (i.e. squared error for regression, or zero-one loss for classification)
- Determine testing error and expected prediction error (most methods effectively measure testing error)
  - Testing error is the prediction error over an independent test sample
  - Expected prediction error is similar, except everything is random, even the training data  - Several models must be built and compared:
  - Split the dataset into three datasets (training, validation, and testing)
    - Training:
      - Model fitting, used for within-model training
      - Error can go to zero
    - Validation:
      - Model selection, used for across-model training
    - Testing:
      - Assessment of the performance of the selected model
      - Has reducible and irreducible error
- Typical splits for datasets are **60%/30%/10%** for training/validation/testing, or **80%/20%** for training/testing
- K-Fold Cross Validation
  - Runs cross-validation multiple times, fixes the problem  of throwing away the validation and testing datasets during training:
    <p align = "center">
    <img src = "https://github.com/adamiller/ist718_notes/blob/master/markdown/image/k-fold.PNG" width = 40%>
    </p>
- Loss functions for validation are not always the same as those used during model fitting
  -i.e. Might use **MSE** in order to fit models with gradient descent, but then use **Mean Absolute Deviation (MAD)** when performing
  model selection
### Bias-Variance Decomposition ###
- It is impossible to know the irreducible error, bias, and variance decomposition
- Want to find the model that minimizes bias and variance
- Mathematically, it is the sum of the Irreducible error, the square of the bias, and the variance:
  <p align = "center">
  <img src = "https://github.com/adamiller/ist718_notes/blob/master/markdown/image/BVD.PNG" width = 40%>
  </p>
- Bias and variance is a fundamental tradeoff, high variance results in an overfit model, and high bias results in an underfit
model; it is best to find the value at which they intersect
### Derivation for Bias-Variance Decomposition ###
  <p align = "center">
  <img src = "https://github.com/adamiller/ist718_notes/blob/master/markdown/image/BVD_derivation_pt1.jpg" width = 40%>  <img src = "https://github.com/adamiller/ist718_notes/blob/master/markdown/image/BVD_derivation_pt2.jpg" width = 40%>
  </p>

