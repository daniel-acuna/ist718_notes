
# Unsupervised Learning

## Scribers: Rohan Nitin Mahajan, Jan Lennart Zeugner.


### Recommendation System:
- Seeks to predict/match user preferences, e.g. Amazon, Youtube, Netflix
- There are multiple types of Recommendation Systems:
    - Collaborative filtering
    - Content based filter
- This class covers a movie recommendation system using content based filtering
- Movies have high dimensions -> I.e. audio and pixels
- In a high dimensional space clustering becomes really hard
    - Generally, the distance between close and far points becomes smaller and smaller with the number of dimensions
    - In a high dimensional space, all movies are very close
- Therefore, we are mapping high dimensions into a low dimensional space and recommend movies based on distance to other movies in a low dimensional space


### Dimensionality Reduction:

- Reducing the number of random variables by obtaining a set of principal variables, while trying to maintain structure/properties of the original data.


<center><img src="IST 718 image12.PNG" width="50%" align="center"></center>  

$$V(n)=\frac{\pi^{\frac{n}{2}}}{\Gamma\left(\frac{n}{2} + 1 \right)}$$


- As we increase the dimensions, volume increases as well.
- However, if dimensions increase too much, noise increases as well and it becomes difficult to recommend



### Dimensionality Reduction Continued

- **Distance Matters:** In a low dimensional space, elements that are really different should be far apart, while elements that are very similar should be very close to each other. 
- Therefore, we need to be able to calculate the distance between two vectors/elements.

- Typical distances between vectors:
  - Euclidian:  
  $$d(v,w) = \sum(v_i-w_i)^2$$  
  
  - Manhattan distance:  
  $$d(v,w) = \sum \mid v_i-w_i \mid$$  
  
  - Cosine distance:  
  $$d(v,w)=\frac{v \cdot w}{\|v\|\|w\|}=\frac{\sum v_iw_i}{\sqrt(\sum v_i^2) \sqrt(\sum w_i^2)}$$

### Principal Component Analysis:

- Linear mapping/transformation of features from the original data into a low dimensional space
- Each principal component is a linear combination of the high dimensional features with maximum variance
- Each principal component has to be uncorrelated of its previous principal component and, therefore, has to run orthogonal to its previous principal component. 
- When performing PCA, data has to be centered


PCA Constraint:   $$\sum\phi_{i1}^2 = 1 \quad\text{and}\quad x'_i = x_i - \overline{x}_i$$
- Otherwise we could increase the variance captured infinitively 

<center><img src="IST718_image1.png" width="50%" align="center"></center>  


   <center> + -> Positive projections </center>  
   <center> - -> Negative projections</center>  
   
  

#### Example of Principal Components:
- The 1st principal component, Z1, runs centrally through the data to capture maximum variance
- The 2nd principal component, Z2, runs orthogonal (perpendicular) to its previous principal component (Z1) to ensure no correlation exists between the two. 

- The histogram of principal component, Z1, shows a wider distribution than the histogram of 2nd principal component, Z2, meaning Z1 has a greater variance captured than Z2.

- In general, every additional  principal component will capture less variance than its previous principal component.

$$\text{var}(Z_1) > \text{var}(Z_2) > \cdots >\text{var}(Z_m)$$



### Example: Running PCA on Diabetes Dataset

- Dataset: 400 datapoints, 10 features
  
<br>
<center><img src="ISt 718 image2.PNG" width="100%" align="center"></center>
    
 

 #### Interpretation:
- The weights of the principal components (vector $\phi_{i1}$) are called loadings
- The biggest absolute value/loading is the most important feature for the prinipal component

##### 1st Principal Component:

- Glucose has the biggest absolute value and, therefore, is the most important feature of PC1
    - If two people have different glucose levels, their data points will lie far apart within PC1
- Furthermore, we notice that BMI as well as age have relatively high absolute values/loadings
- We could categorize the most highest loadings into a new class called "health"

<center>$Z_1 = \phi_{11}x'_1 + \phi_{21}x'_2 + \cdots + \phi_{m1}x'_m$ </center>
<center>$Z_1 = -0.48 * age - 0.36* sex - 0.51 * bmi - 0.60 * glu$</center>

##### 2nd Principal Component:
- Biggest absolute value and, thus, most relevant for principal component one is sex/gender
- We also notice that the featues most dominant in PC1 are less dominant in PC1

<center>$Z_2 = -0.17 * age - 0.80* sex - 0.53 * bmi - 0.17 * glu$</center>
    




### Linear Algebra

- We can not only map a high dimensional space into a low dimensional space, but we can also do the opposite - map low dimensional space to high dimensional space

##### Example: Mnist Image Data
- We map the mnist image dataset from a low dimensional space into a high dimensional space and make images clearer.
- The fewer principal components used, the smaller the variance captured from the original dataset. 
    - We destroy the essence of the original data
    - Therefore, the images of the mnist dataset are less clear with only 1 or two principal components 

### How do we know how many principal components to select ? 

<br>
<center><img src="IST 718 image3.PNG" width="70%" align="center"></center>

- Select the elbow point
    - In other words, select the point where the additional/margina varianced gained becomes minimal


### Latent Dirichlet Allocation (LDA):

- LDA is commonly used in natural language processing
- Uses matrix factorization
- LDA makes stronger assumptions about the distributions as they need to be probabilities.  
- Hard to validate


### Clustering K-Means
- Clusters should contain similar elements
    - Distance between elements within a cluster should be small
    - Distance between different clusters, however, should be large
    
    
<center><img src="IST 718 image4.PNG" width="70%" align="center"></center>
