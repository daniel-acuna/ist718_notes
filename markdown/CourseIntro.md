
# Course Introduction

Lecturer: Prof. Daniel Acuña  
Scriber: Lizhen Liang & Yimin Xiao  Lecture 1 ----- 1/15/2019

## 1. About this course

### 1.1 Objectives

-   Develop predictive models that are interpretable.
    
-   Understand oppotunities / challenges of big data.
    
-   Understanding why / how big data increases accuracy but lowers interpretability.
    
-   Understand the statistical bias, variance, and intrisic noise.
    
-   Understand model fitting, selection, and estimation of generalization error.
    

### 1.2 Course content

-   1 / 4 of the course covers prerequisite skills for big data analytics: python programming, linear algebra, calculus and statistics.
    
-   1 / 4 of the course covers the Spark and Hadoop, providing skills required to perform big data analytics.
    
-   1 / 4 of the course consists of case studies, where you apply your skills and knowledge to real-world applications.
    
-   1 / 4 of the course consists of a project, where you work in groups in real world application.
    

### 1.3 Focus
![image0](image/0.png)
We will be focusing on the diagnostic, descriptive and predictive aspects.

## 2. What is data science?

With the goal of using data to make decisions and drive actions, data science is a combination of:

- Information / computer science

- Mathematics

- Statistics

- Research / Management Science

- Domain Knowledge

According to the Venn Diagram, data science is the overlapping area of hacking skills, math & statistics knowledge and domain knowledge:
![image1](https://github.com/sciosci/ist718_notes/blob/master/markdown/image/1.png)

### 2.1 The “classic” and “new” kinds of data science

The classic kind of data science means a bunch of experts, in charge of creating relatively small and interpretable models, providing features to describe the dataset or do predictions. The accuracy of the models created by classic data scientist cannot be proved.

By contrast, the new kind of data science need no expert for a certain domain. Models are generalized and takes data with features of low level. For example, in old days, experts generate features from raw transaction data that describes a credit card user. But nowadays, experts simply use the raw transaction data as the input data for the model.

Models that are used for the new kind of data science are generally black boxes: they are hard to explain.

## 3 What is big data?

According to a study given by Andrew Ng and Michael I. Jordon, when the dataset is small, a simpler model has smaller error rate than a more complicated model. But when the size of a dataset gets bigger, the error rate of the more complicated model is smaller than the simpler model.

Big data means data with large volume, fast velocity and complex data variety (“three V” for big data).

Since big data are usually too big to store on a single system, too fast to be processed by a single computer and too complex for traditional processing techniques, big data are usually stored and processed on a distributed system.

## 4 Example for big data applications

- Recommendation system

- Activity recognition

- Image recogniiton

- Speech recognition
