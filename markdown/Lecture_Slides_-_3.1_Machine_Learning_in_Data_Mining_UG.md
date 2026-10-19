## Slide 1
### Lecture 6: Machine Learning in Data Mining

3031ICT: Applied Data Mining  
3804ICT: Data Mining

Dr Can Wang  
School of Information and Communication Technology

## Slide 2
### Machine Learning in Data Mining

- Machine Learning Basics
  - Basic Concepts
  - Evaluation, Overfitting & underfitting, Cross Validation
- Supervised Machine Learning Methods
  - Decision Tree Induction
  - Bayes Classification Methods
- Un-Supervised Machine Learning Methods
  - Clustering Basics
  - Partition Clustering: K-Means Clustering

## Slide 3
### Supervised vs. Unsupervised Learning

- Supervised learning (example: classification)
  - Supervision: The training data (observations, measurements, etc.) are accompanied by labels indicating the class of the observations.
  - New data is classified based on the training set.
- Unsupervised learning (example: clustering)
  - The class labels of training data is unknown.
  - Given a set of measurements, observations, etc., with the aim of establishing the existence of classes or clusters in the data.

## Slide 4
### Prediction Problems: Classification vs. Numeric Prediction

- Classification
  - Predicts categorical class labels (discrete or nominal)
  - Classifies data (constructs a model) based on the training set and the values (class labels) in a classifying attribute, and uses it in classifying new data
- Numerical Prediction
  - Models continuous-valued functions, i.e., predicts unknown or missing values
- Typical applications
  - Credit/loan approval:
  - Medical diagnosis: if a tumor is cancerous or benign
  - Fraud detection: if a transaction is fraudulent
  - Web page categorization: which category it is

## Slide 5
### Classification—A Two-Step Process

- Model construction: describing a set of predetermined classes
  - Each tuple/sample is assumed to belong to a predefined class, as determined by the class label attribute (decision attribute).
  - The set of tuples used for model construction is training set.
- Model usage: for classifying future or unknown objects
  - Estimate accuracy of the model
    - The known label of test sample is compared with the classified result from the model.
    - Accuracy rate is the percentage of test set samples that are correctly classified.
    - Test set is independent of training set (otherwise overfitting).
  - If the accuracy is acceptable, use the model to classify new data.

## Slide 6
### General Approach for Building Classification Model

Training Set:

| Tid | Attrib1 | Attrib2 | Attrib3 | Class |
| --- | --- | --- | --- | --- |
| 1 | Yes | Large | 125K | No |
| 2 | No | Medium | 100K | No |
| 3 | No | Small | 70K | No |
| 4 | Yes | Medium | 120K | No |
| 5 | No | Large | 95K | Yes |
| 6 | No | Medium | 60K | No |
| 7 | Yes | Large | 220K | No |
| 8 | No | Small | 85K | Yes |
| 9 | No | Medium | 75K | No |
| 10 | No | Small | 90K | Yes |

Test Set:

| Tid | Attrib1 | Attrib2 | Attrib3 | Class |
| --- | --- | --- | --- | --- |
| 11 | No | Small | 55K | ? |
| 12 | Yes | Medium | 80K | ? |
| 13 | Yes | Large | 110K | ? |
| 14 | No | Small | 95K | ? |
| 15 | No | Large | 67K | ? |

[Figure: Process I — Induction: Training Set → Learning algorithm → Learn Model → Model. Process II — Deduction: Model and Test Set → Apply Model. Arrows show learning a model from labeled data and applying it to unlabeled test data.]

## Slide 7
### Evaluating Classification Methods

- Predictive accuracy:

  $$\operatorname{Accuracy}=\frac{\text{Number of correct classifications}}{\text{Total number of test cases}}$$

- Efficiency:
  - Time to construct the model
  - Time to use the model
- Robustness: the ability to handle noise and missing values
- Scalability: efficiency when data size increases
- Interpretability:
  - Understandability and insight provided by the model
- Compactness of the model: size of the tree, or the number of rules.

## Slide 8
### Evaluation Methods

- The available dataset D is divided into two disjoint subsets
  - The training set $D_{\text{train}}$ (for learning a model)
  - The test set $D_{\text{test}}$ (for testing the model)
- Important: training set should not be used in testing and the test set should not be used in learning.
  - Unseen test set provides an unbiased estimate of accuracy.
- The test set is also called the holdout set (If the examples in the original dataset D are all labeled with classes).

## Slide 9
### Precision and Recall Measures

- Used in information retrieval and text classification.
- We use a confusion matrix to introduce them.

| | Classified Positive | Classified Negative |
| --- | --- | --- |
| Actual Positive | TP | FN |
| Actual Negative | FP | TN |

where:

- TP: the number of correct classifications of the positive examples (true positive),
- FN: the number of incorrect classifications of positive examples (false negative),
- FP: the number of incorrect classifications of negative examples (false positive), and
- TN: the number of correct classifications of negative examples (true negative).

## Slide 10
### Precision and Recall Measures (cont…)

| | Classified Positive | Classified Negative |
| --- | --- | --- |
| Actual Positive | TP | FN |
| Actual Negative | FP | TN |

$$
p=\frac{TP}{TP+FP},\qquad r=\frac{TP}{TP+FN}.
$$

- Precision p is the number of correctly classified positive examples divided by the total number of examples that are classified as positive.
- Recall r is the number of correctly classified positive examples divided by the total number of actual positive examples in the test set.

## Slide 11
### F1-Score

- It is hard to compare two classifiers using two measures. F1 score combines precision and recall into one measure.

$$F_1=\frac{2pr}{p+r}$$

F1-score is the harmonic mean of precision and recall.

$$F_1=\frac{2}{\frac1p+\frac1r}$$

- The harmonic mean of two numbers tends to be closer to the smaller of the two.
- If F1-value is large, both p and r must be large.

## Slide 12
### Underfitting and Overfitting

- Training errors: the number of classification errors on training records.
- Generalization (test) errors: the number of classification errors on test records.
- A good model should have low errors of both types.
- Model underfitting: model is too simple such that both Training error and Generalization error are high.
- Model overfitting: A model that fits the training data too well (with too low training errors) but may have a poorer generalization error than a model with higher training error.

## Slide 13
### Underfitting

- Too high training errors

[Figure: Two scatter plots of two classes, represented by different point symbols, illustrate overly simple decision boundaries that fail to separate the classes. Fine point positions and numerical tick labels are not reproduced; OCR of the image does not recover additional meaningful annotations.]

Models are too simple!

## Slide 14
### Overfitting

- Overfitting due to noise
  - Decision boundary is distorted by noise point.
- Overfitting due to insufficient data
  - Lack of data points makes it difficult to draw the decision boundary (border line between two neighboring regions of different classes).

[Figure: Two classification diagrams show how an isolated noise point distorts a boundary, and how sparse observations leave the boundary between classes uncertain. Points use different symbols for the classes; exact point coordinates and boundary geometry are not reproduced.]

## Slide 15
### Evaluation methods (cont…)

- n-fold cross-validation: The available data is partitioned into n equal-size disjoint subsets.
- Use each subset as the test set and combine the rest n−1 subsets as the training set to learn a classifier.
- The procedure runs n times, which give n accuracies.
- The final estimated accuracy of learning is the average of the n accuracies.
- 10-fold and 5-fold cross-validations are commonly used (take turns to be test set). This method is used when the available data is large.

## Slide 16
### Evaluation methods (cont…)

- Leave-one-out cross-validation: This method is used when the data set is very small.
- It is a special case of n-fold cross-validation (Here, n is the number of data objects).
- Each fold of the cross validation has only a single test example and all the rest of the data is used in training.
- If the original data has n examples, this is n-fold cross-validation.

## Slide 17
### Machine Learning in Data Mining

- Machine Learning Basics
  - Basic Concepts
  - Evaluation, Overfitting & underfitting, Cross Validation
- Supervised Machine Learning Methods
  - Decision Tree Induction
  - Bayes Classification Methods
- Un-Supervised Machine Learning Methods
  - Clustering Basics
  - Partition Clustering: K-Means Clustering

## Slide 18
### Decision Tree

- Decision tree learning is one of the most widely used techniques for classification.
  - Its classification accuracy is competitive with other methods, and
  - It is very efficient.
- The classification model is a tree, called decision tree.
- C4.5 by Ross Quinlan is perhaps the best known system. It can be downloaded from the Web.

## Slide 19
### Example of a Decision Tree

Training Data:

| ID | Home Owner | Marital Status | Annual Income | Defaulted Borrower |
| --- | --- | --- | --- | --- |
| 1 | Yes | Single | 125K | No |
| 2 | No | Married | 100K | No |
| 3 | No | Single | 70K | No |
| 4 | Yes | Married | 120K | No |
| 5 | No | Divorced | 95K | Yes |
| 6 | No | Married | 60K | No |
| 7 | Yes | Divorced | 220K | No |
| 8 | No | Single | 85K | Yes |
| 9 | No | Married | 75K | No |
| 10 | No | Single | 90K | Yes |

[Figure: Model: Decision Tree. “Splitting Attributes” identifies the internal nodes Home Owner, MarSt, and Income. Branches and leaf labels are transcribed below.]

- Home Owner
  - Yes → NO
  - No → MarSt
    - Married → NO
    - Single, Divorced → Income
      - < 80K → NO
      - > 80K → YES

## Slide 20
### Another Example of Decision Tree

| ID | Home Owner | Marital Status | Annual Income | Defaulted Borrower |
| --- | --- | --- | --- | --- |
| 1 | Yes | Single | 125K | No |
| 2 | No | Married | 100K | No |
| 3 | No | Single | 70K | No |
| 4 | Yes | Married | 120K | No |
| 5 | No | Divorced | 95K | Yes |
| 6 | No | Married | 60K | No |
| 7 | Yes | Divorced | 220K | No |
| 8 | No | Single | 85K | Yes |
| 9 | No | Married | 75K | No |
| 10 | No | Single | 90K | Yes |

[Figure: Alternative decision tree with MarSt as the root.]

- MarSt
  - Married → NO
  - Single, Divorced → Home Owner
    - Yes → NO
    - No → Income
      - < 80K → NO
      - > 80K → YES

There could be more than one tree that fits the same data!

## Slide 21
### Apply Model to Test Data

Test Data:

| Home Owner | Marital Status | Annual Income | Defaulted Borrower |
| --- | --- | --- | --- |
| No | Married | 80K | ? |

Start from the root of tree.

[Figure: Decision tree for the test record; this page begins traversal at Home Owner.]

- Home Owner
  - Yes → NO
  - No → MarSt
    - Married → NO
    - Single, Divorced → Income
      - < 80K → NO
      - > 80K → YES

## Slide 22
### Apply Model to Test Data

Test Data:

| Home Owner | Marital Status | Annual Income | Defaulted Borrower |
| --- | --- | --- | --- |
| No | Married | 80K | ? |

[Figure: Next animation stage of the same test-record traversal, highlighting the Home Owner root.]

- Home Owner
  - Yes → NO
  - No → MarSt
    - Married → NO
    - Single, Divorced → Income
      - < 80K → NO
      - > 80K → YES

## Slide 23
### Apply Model to Test Data

Test Data:

| Home Owner | Marital Status | Annual Income | Defaulted Borrower |
| --- | --- | --- | --- |
| No | Married | 80K | ? |

[Figure: Home Owner = No is highlighted in the test row and on the No branch toward MarSt.]

- Home Owner
  - Yes → NO
  - No → MarSt
    - Married → NO
    - Single, Divorced → Income
      - < 80K → NO
      - > 80K → YES

## Slide 24
### Apply Model to Test Data

Test Data:

| Home Owner | Marital Status | Annual Income | Defaulted Borrower |
| --- | --- | --- | --- |
| No | Married | 80K | ? |

[Figure: Traversal continues from Home Owner = No to the MarSt splitting node.]

- Home Owner
  - Yes → NO
  - No → MarSt
    - Married → NO
    - Single, Divorced → Income
      - < 80K → NO
      - > 80K → YES

## Slide 25
### Apply Model to Test Data

Test Data:

| Home Owner | Marital Status | Annual Income | Defaulted Borrower |
| --- | --- | --- | --- |
| No | Married | 80K | ? |

[Figure: Home Owner = No and Marital Status = Married are highlighted. The Married branch leads to the NO leaf.]

- Home Owner
  - Yes → NO
  - No → MarSt
    - Married → NO
    - Single, Divorced → Income
      - < 80K → NO
      - > 80K → YES

## Slide 26
### Apply Model to Test Data

Test Data:

| Home Owner | Marital Status | Annual Income | Defaulted Borrower |
| --- | --- | --- | --- |
| No | Married | 80K | ? |

Assign Defaulted to “No”.

[Figure: Completed traversal: Home Owner = No → MarSt = Married → NO.]

- Home Owner
  - Yes → NO
  - No → MarSt
    - Married → NO
    - Single, Divorced → Income
      - < 80K → NO
      - > 80K → YES

## Slide 27
### Decision Tree Classification Task

Training Set:

| Tid | Attrib1 | Attrib2 | Attrib3 | Class |
| --- | --- | --- | --- | --- |
| 1 | Yes | Large | 125K | No |
| 2 | No | Medium | 100K | No |
| 3 | No | Small | 70K | No |
| 4 | Yes | Medium | 120K | No |
| 5 | No | Large | 95K | Yes |
| 6 | No | Medium | 60K | No |
| 7 | Yes | Large | 220K | No |
| 8 | No | Small | 85K | Yes |
| 9 | No | Medium | 75K | No |
| 10 | No | Small | 90K | Yes |

Test Set:

| Tid | Attrib1 | Attrib2 | Attrib3 | Class |
| --- | --- | --- | --- | --- |
| 11 | No | Small | 55K | ? |
| 12 | Yes | Medium | 80K | ? |
| 13 | Yes | Large | 110K | ? |
| 14 | No | Small | 95K | ? |
| 15 | No | Large | 67K | ? |

[Figure: Training Set → Tree Induction algorithm → Learn Model → Model (Decision Tree), labeled Induction. The Model and Test Set feed Apply Model, labeled Deduction.]

## Slide 28
### Machine Learning in Data Mining

- Machine Learning Basics
  - Basic Concepts
  - Evaluation, Overfitting & underfitting, Cross Validation
- Supervised Machine Learning Methods
  - Decision Tree Induction
  - Bayes Classification Methods
- Un-Supervised Machine Learning Methods
  - Clustering Basics
  - Partition Clustering: K-Means Clustering

## Slide 29
### Bayesian Classification: Why?

- A statistical classifier: performs probabilistic prediction, i.e., predicts class membership probabilities
- Foundation: Based on Bayes’ Theorem.
- Performance: A simple Bayesian classifier, naïve Bayesian classifier, has comparable performance with decision tree and selected neural network classifiers
- Incremental: Each training example can incrementally increase/decrease the probability that a hypothesis is correct — prior knowledge can be combined with observed data
- Standard: Even when Bayesian methods are computationally intractable, they can provide a standard of optimal decision making against which other methods can be measured

## Slide 30
### Bayes Classifier

A probabilistic framework for solving classification problems

Conditional Probability:

$$P(Y\mid X)=\frac{P(X,Y)}{P(X)}$$

$$P(X\mid Y)=\frac{P(X,Y)}{P(Y)}$$

Bayes theorem:

$$P(Y\mid X)=\frac{P(X\mid Y)P(Y)}{P(X)}$$

## Slide 31
### Bayes Classifier

- Given new value of attributes $a_1,\ldots,a_n$, estimate the probabilities of the class attribute taking each possible value. Choose the value with the maximum probability.

| Tid | Refund | Marital Status | Taxable Income | Cheat |
| --- | --- | --- | --- | --- |
| 1 | Yes | Single | 125K | No |
| 2 | No | Married | 100K | No |
| 3 | No | Single | 70K | No |
| 4 | Yes | Married | 120K | No |
| 5 | No | Divorced | 95K | Yes |
| 6 | No | Married | 60K | No |
| 7 | Yes | Divorced | 220K | No |
| 8 | No | Single | 85K | Yes |
| 9 | No | Married | 75K | No |
| 10 | No | Single | 90K | Yes |

| Refund | Marital Status | Taxable Income | Cheat |
| --- | --- | --- | --- |
| No | Married | 80K | ? |

Estimate conditional probabilities:

$$P_1=P(\text{cheat=yes}\mid\text{Ref=No, MS=Married, Income=80})$$

$$P_2=P(\text{cheat=No}\mid\text{Ref=No, MS=Married, Income=80})$$

How to estimate the probabilities?

If $P_1>P_2$, classify as cheat, otherwise no cheat.

## Slide 32
### Bayes Classifier

- Given feature vector $A=(a_1,\ldots,a_n)$, how to estimate the probability $P(c\mid A)$?
  - E.g., how to estimate $P(\text{cheat=yes}\mid\text{Refund=No, MStatus=Married, Income=80})$ or shorthand: $P(\text{yes}\mid(\text{No, Married, 80}))$?
- Use the Bayes theorem

  $$P(c\mid A)=\frac{P(A\mid c)P(c)}{P(A)}$$

- $P(c)$ can be estimated as the fraction of training records taking class value c, i.e., $P(c)=N_c/N$, where N is the total number of training records, $N_c$ is the number of records in class c.
- No need to estimate $P(A)$ for comparisons of $P(c_1\mid A)$ and $P(c_2\mid A)$.
- Thus, the problem is “how to estimate $P(A\mid c_k)P(c_k)$”?

## Slide 33
### Bayes Classifier

- Assume the features $a_1,\ldots,a_n$ are independent, given c classes, thus

Use Chain Rule, then we have:

$$
\begin{aligned}
P(C_k)P(A\mid C_k)
&=P(A,C_k)=P(a_1,\ldots,a_n,C_k)\\
&=P(a_1\mid a_2,\ldots,a_n,C_k)\times P(a_2,\ldots,a_n,C_k)\\
&=P(a_1\mid a_2,\ldots,a_n,C_k)\times P(a_2\mid a_3,\ldots,a_n,C_k)P(a_3,\ldots,a_n,C_k)\\
&=\cdots\\
&=P(a_1\mid a_2,\ldots,a_n,C_k)\times P(a_2\mid a_3,\ldots,a_n,C_k)
\times\cdots\times P(a_{n-1}\mid a_n,C_k)\times P(a_n\mid C_k)\times P(C_k)\\
&=P(a_1\mid C_k)\times P(a_2\mid C_k)\times\cdots\times P(a_n\mid C_k)\times P(C_k)\\
&=P(C_k)\prod_{i=1}^{n}P(a_i\mid C_k).
\end{aligned}
$$

Independent Features:

$$P(C_k)=\frac{N_k}{N},\qquad P(a_i\mid C_k)=\frac{N_{ik}}{N_k}$$

- N: Total number of data
- $N_k$: Total number of k-th class data
- $N_{ik}$: Total number of i-th feature in the k-th class data

## Slide 34
### Bayes Classifier

Assume the features $a_1,\ldots,a_n$ are independent given class c. Thus:

Use Chain Rule, then we have:

$$
\begin{aligned}
P(C_k)P(A\mid C_k)
&=P(A,C_k)\\
&=P(a_1,\ldots,a_n,C_k)\\
&=P(a_1\mid a_2,\ldots,a_n,C_k)\times P(a_2,\ldots,a_n,C_k)\\
&=P(a_1\mid a_2,\ldots,a_n,C_k)\times P(a_2\mid a_3,\ldots,a_n,C_k)P(a_3,\ldots,a_n,C_k)\\
&=\cdots\\
&=P(a_1\mid a_2,\ldots,a_n,C_k)\times P(a_2\mid a_3,\ldots,a_n,C_k)
\times\cdots\times P(a_{n-1}\mid a_n,C_k)\times P(a_n\mid C_k)\times P(C_k)\\
&=P(a_1\mid C_k)\times P(a_2\mid C_k)\times\cdots\times P(a_n\mid C_k)\times P(C_k)\\
&=P(C_k)\prod_{i=1}^{n}P(a_i\mid C_k).
\end{aligned}
$$

Independent Features:

$$P(C_k)=\frac{N_k}{N},\qquad P(a_i\mid C_k)=\frac{N_{ik}}{N_k}$$

- N: Total number of data
- $N_k$: Total number of k-th class data
- $N_{ik}$: Total number of i-th feature in the k-th class data

## Slide 35
### Bayes Classifier Example

| Name | Give Birth | Can Fly | Live in Water | Have Legs | Class |
| --- | --- | --- | --- | --- | --- |
| human | yes | no | no | yes | mammals |
| python | no | no | no | no | non-mammals |
| salmon | no | no | yes | no | non-mammals |
| whale | yes | no | yes | no | mammals |
| frog | no | no | sometimes | yes | non-mammals |
| komodo | no | no | no | yes | non-mammals |
| bat | yes | yes | no | yes | mammals |
| pigeon | no | yes | no | yes | non-mammals |
| cat | yes | no | no | yes | mammals |
| leopard shark | yes | no | yes | no | non-mammals |
| turtle | no | no | sometimes | yes | non-mammals |
| penguin | no | no | sometimes | yes | non-mammals |
| porcupine | yes | no | no | yes | mammals |
| eel | no | no | yes | no | non-mammals |
| salamander | no | no | sometimes | yes | non-mammals |
| gila monster | no | no | no | yes | non-mammals |
| platypus | no | no | no | yes | mammals |
| owl | no | yes | no | yes | non-mammals |
| dolphin | yes | no | yes | no | mammals |
| eagle | no | yes | no | yes | non-mammals |

Test data: A: (yes, no, yes, no)

| Give Birth | Can Fly | Live in Water | Have Legs | Class |
| --- | --- | --- | --- | --- |
| yes | no | yes | no | ? |

M: mammals  
N: non-mammals

$$P(A\mid M)P(M)\quad\text{vs}\quad P(A\mid N)P(N)$$

$$P(A\mid M)=\frac67\times\frac67\times\frac27\times\frac27=0.06$$

$$P(A\mid N)=\frac1{13}\times\frac{10}{13}\times\frac3{13}\times\frac4{13}=0.0042$$

$$P(A\mid M)P(M)=0.06\times\frac7{20}=0.021$$

$$P(A\mid N)P(N)=0.0042\times\frac{13}{20}=0.0027$$

$$P(A\mid M)P(M)>P(A\mid N)P(N)$$

⇒ Mammals

## Slide 36
### Machine Learning in Data Mining

- Machine Learning Basics
  - Basic Concepts
  - Evaluation, Overfitting & underfitting, Cross Validation
- Supervised Machine Learning Methods
  - Decision Tree Induction
  - Bayes Classification Methods
- Un-Supervised Machine Learning Methods
  - Clustering Basics
  - Partition Clustering: K-Means Clustering

## Slide 37
### What is Cluster Analysis?

- Cluster: A collection of data objects
  - Similar (or related) to one another within the same group
  - Dissimilar (or unrelated) to the objects in other groups
- Cluster analysis (or clustering, data segmentation, …)
  - Finding similarities between data according to the characteristics found in the data and grouping similar data objects into clusters
- Unsupervised learning: no predefined classes (i.e., learning by observations vs. learning by examples: supervised)
- Typical applications
  - As a stand-alone tool to get insight into data distribution
  - As a preprocessing step for other algorithms

## Slide 38
### Clustering for Data Understanding and Applications

- Biology: taxonomy of living things -- kingdom, phylum, class, order, family, genus and species
- Information retrieval: document clustering
- Land use: Identification of areas of similar land use in an earth observation database
- Marketing: Help marketers discover distinct groups in their customer bases, and then use this knowledge to develop targeted marketing programs
- City-planning: Identifying groups of houses according to their house type, value, and geographical location
- Earth-quake studies: Observed earthquake epicenters should be clustered along continent faults
- Climate: understanding earth climate, find patterns of atmosphere and ocean
- Economic Science: market research

## Slide 39
### Quality: What Is Good Clustering?

- A good clustering method will produce high quality clusters
  - High intra-class similarity: cohesive within clusters
  - Low inter-class similarity: distinctive between clusters
- The quality of a clustering method depends on
  - The similarity measure used by the method
  - Its implementation, and
  - Its ability to discover some or all of the hidden patterns

## Slide 40
### Distance between Clusters

- Single link: the smallest distance between an element in one cluster and an element in the other, i.e., $\operatorname{dist}(K_i,K_j)=\min(t_{ip},t_{jq})$
- Complete link: the largest distance between an element in one cluster and an element in the other, i.e., $\operatorname{dist}(K_i,K_j)=\max(t_{ip},t_{jq})$
- Average: the avg distance between an element in one cluster and an element in the other, i.e., $\operatorname{dist}(K_i,K_j)=\operatorname{avg}(t_{ip},t_{jq})$
- Centroid: the distance between the centroids of two clusters, i.e., $\operatorname{dist}(K_i,K_j)=\operatorname{dist}(C_i,C_j)$
- Medoid: the distance between the medoids of two clusters, i.e., $\operatorname{dist}(K_i,K_j)=\operatorname{dist}(M_i,M_j)$
  - Medoid: a chosen, centrally located object in the cluster

[Figure: Cluster-distance sketches mark representative points with X. An accompanying “Centroid of a triangle” diagram illustrates a geometric centroid. Exact positions and graphical connecting lines are not reproduced.]

## Slide 41
### Major Clustering Approaches (I)

- Partitioning approach:
  - Construct various partitions and then evaluate them by some criterion, e.g., minimizing the sum of square errors
  - Typical methods: k-means, k-medoids, CLARANS
- Hierarchical approach:
  - Create a hierarchical decomposition of the set of data (or objects) using some criterion
  - Typical methods: Diana, Agnes, BIRCH, CAMELEON
- Density-based approach:
  - Based on connectivity and density functions
  - Typical methods: DBSCAN, OPTICS, DenClue
- Grid-based approach:
  - Based on a multiple-level granularity structure
  - Typical methods: STING, WaveCluster, CLIQUE

## Slide 42
### Major Clustering Approaches (II)

- Model-based clustering:
  - A model is hypothesized for each of the clusters and tries to find the best fit of that model to each other
  - Typical methods: EM, SOM, COBWEB
- Frequent pattern-based clustering:
  - Based on the analysis of frequent patterns
  - Typical methods: p-Cluster
- User-guided or constraint-based clustering:
  - Clustering by considering user-specified or application-specific constraints
  - Typical methods: COD (obstacles), constrained clustering
- Link-based clustering:
  - Objects are often linked together in various ways
  - Massive links can be used to cluster objects: SimRank, LinkClus

## Slide 43
### Machine Learning in Data Mining

- Machine Learning Basics
  - Basic Concepts
  - Evaluation, Overfitting & underfitting, Cross Validation
- Supervised Machine Learning Methods
  - Decision Tree Induction
  - Bayes Classification Methods
- Un-Supervised Machine Learning Methods
  - Clustering Basics
  - Partition Clustering: K-Means Clustering

## Slide 44
### Partitioning Algorithms

- Partitioning method: Partitioning a database D of n objects into a set of k clusters, such that the sum of squared distances is minimized (where $c_i$ is the centroid or medoid of cluster $C_i$)

$$E=\sum_{i=1}^{k}\sum_{p\in C_i}(p-c_i)^2$$

- Given k, the k-means algorithm is implemented in four steps:
  1. Partition objects into k nonempty subsets.
  2. Compute seed points as the centroids of the clusters of the current partitioning (the centroid is the center, i.e., mean point, of the cluster).
  3. Assign each object to the cluster with the nearest seed point.
  4. Go back to Step 2, stop when the assignment does not change.

## Slide 45
### An Example of K-Means Clustering

K=2

[Figure: A sequence of two-dimensional point plots shows “The initial data set” → “Randomly partition objects into k groups” → “Update the cluster centroids” → “Reassign objects” → “Update the cluster centroids”, with “Loop if needed”. Different point symbols distinguish the two groups and centroid marks indicate their centers. Exact point positions and the graphical changes between iterations cannot be reproduced as text; OCR was attempted to recover labels.]

- Partition objects into k nonempty subsets
- Repeat
  - Compute centroid (i.e., mean point) for each partition
  - Assign each object to the cluster of its nearest centroid
- Until no change

## Slide 46
### Machine Learning in Data Mining

- Machine Learning Basics
  - Basic Concepts
  - Evaluation, Overfitting & underfitting, Cross Validation
- Supervised Machine Learning Methods
  - Decision Tree Induction
  - Bayes Classification Methods
- Un-Supervised Machine Learning Methods
  - Clustering Basics
  - Partition Clustering: K-Means Clustering

## Slide 47
### Have a question?
