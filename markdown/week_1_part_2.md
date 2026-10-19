## Slide 1
### Lecture Week 2: Data Exploration and Data Pre-processing

3031ICT: Applied Data Mining  
3804ICT: Data Mining

Dr Can Wang  
School of Information and Communication Technology

## Slide 2
### Contents

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualization.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Data Cleaning.
  - Data Integration.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 3
### Data Objects

- Data sets are made up of data objects.
- A data object represents an entity, also called samples, examples, instances, data points, objects, tuples, observations.
- Data objects are described by attributes.
- Database: rows → data objects; columns → attributes.

[Figure: Example data table with columns labeled “attributes” and rows labeled “objects”.]

| Row | Age | Workclass | Fnlwgt | Education | Education-num | Marital-status | Occupation | Relationship | Race | Sex | Capital-gain | Capital-loss | Hours-per-week | Native-country | Income |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 39 | State-gov | 77516 | Bachelors | 13 | Never-married | Adm-clerical | Not-in-family | White | Male | 2174 | 0 | 40 | United-States | <=50K |
| 1 | 50 | Self-emp-not-inc | 83311 | Bachelors | 13 | Married-civ-spouse | Exec-managerial | Husband | White | Male | 0 | 0 | 13 | United-States | <=50K |
| 2 | 38 | Private | 215646 | HS-grad | 9 | Divorced | Handlers-cleaners | Not-in-family | White | Male | 0 | 0 | 40 | United-States | <=50K |
| 3 | 53 | Private | 234721 | 11th | 7 | Married-civ-spouse | Handlers-cleaners | Husband | Black | Male | 0 | 0 | 40 | United-States | <=50K |
| 4 | 28 | Private | 338409 | Bachelors | 13 | Married-civ-spouse | Prof-specialty | Wife | Black | Female | 0 | 0 | 40 | Cuba | <=50K |

## Slide 4
### Attribute Types

- Nominal Attributes
  - Are “symbols” or “names of things”.
  - Each value represents some kind of category, code, or state, and so nominal attributes are also referred to as categorical. The values do not have any meaningful order.
  - Examples: ID numbers, eye color, zip codes.
- Ordinal Attributes
  - Have a meaningful order or ranking among them.
  - The magnitude between successive values is not known.
  - Examples: rankings (e.g., taste of potato chips on a scale from 1–10), grades, height {tall, medium, short}.
- Interval-scaled attributes
  - Are measured on a scale of equal-size units.
  - Have order and can be positive, 0, or negative.
  - Providing a ranking of values and enable to quantify the difference between values.
  - Examples: calendar dates, temperatures in Celsius or Fahrenheit.
- Ratio-scaled attributes
  - Are numeric with an inherent zero-point. That is, if a measurement is ratio-scaled, we can speak of a value as being a multiple (or ratio) of another value. In addition, the values are ordered, and we can also compute the difference between values, as well as the mean, median, and mode.
  - Examples: temperature in Kelvin, length, time, counts.

## Slide 5
### Discrete vs. Continuous Attributes

- Discrete Attribute
  - Has only a finite or countably infinite set of values.
  - E.g., zip codes, profession, or the set of words in a collection of documents.
  - Sometimes, represented as integer variables.
  - Note: Binary attributes are a special case of discrete attributes.
- Continuous Attribute
  - Has real numbers as attribute values.
  - E.g., temperature, height, or weight.
  - Practically, real values can only be measured and represented using a finite number of digits.
  - Continuous attributes are typically represented as floating-point variables.

## Slide 6
### Data Exploration & Pre-processing

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualization.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Data Cleaning.
  - Data Integration.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 7
### Basic Statistical Descriptions of Data

- Motivation
  - To better understand the data: central tendency, variation and spread.
  - To pre-process your data well, it is essential to have an overall picture of data.
- Basic statistical descriptions
  - Measures of central tendency (where does the values of attribute most fall in?)
    - The location of the middle or centre of a data distribution.
    - We will discuss mean, median, and midrange.
  - Measures of dispersion of the data (how does the values of attribute spread out?)
    - We will discuss range, quartiles, and interquartile range.
    - Five-number summary (min, 25%, median, 75%, max) and boxplot can be used.

## Slide 8
### Measures of Location: Mean and Median

- Mean:
  - The mean is the most common measure of the location of a set of points.
  - However, the mean is very sensitive to outliers.
  - Thus, the median or a trimmed mean is also commonly used.

$$
\bar{x}=\frac{1}{n}\sum_{i=1}^{n}x_i,
\qquad
\bar{x}=\frac{\sum_{i=1}^{n}w_i x_i}{\sum_{i=1}^{n}w_i}.
$$

- Median:
  - Middle value if odd number of values, or average of the middle two values otherwise.
- Midrange:
  - The average of the largest and smallest values in the set.

## Slide 9
### Measures of Spread: Range and Variance I

- Range is the difference between the max and min (i.e. max − min).
- The variance or standard deviation $s_x$ is the most common measure of the spread of a set of points.

Formula shown beside the label “Sample Standard Deviation”:

$$
\operatorname{variance}(x)=s_x^2=\frac{1}{m-1}\sum_{i=1}^{m}(x_i-\bar{x})^2.
$$

- Because of outliers, other measures are often used.

$$
\operatorname{AAD}(x)=\frac{1}{m}\sum_{i=1}^{m}|x_i-\bar{x}|,
$$

$$
\operatorname{MAD}(x)=\operatorname{median}\left(\{|x_1-\tilde{x}|,\ldots,|x_m-\tilde{x}|\}\right),
$$

$$
\operatorname{interquartile\ range}(x)=x_{75\%}-x_{25\%}.
$$

## Slide 10
### Measures of Spread: Range and Variance II

- Range
  - Difference between the largest (max()) and smallest (min()) values: max − min.
- Quartiles
  - Quartiles are points taken at regular intervals of a data distribution, dividing it into essentially equal-sized consecutive sets. (Note: there may not be data values of X that divide the data into exactly equal-sized subsets, then round up to the next integer.)
  - Q1 (25th percentile): splits off the lowest 25% of data from the highest 75%.
  - Q3 (75th percentile): splits off the highest 25% of data from the lowest 75%.
- Inter-Quartile Range: IQR = Q3 − Q1.
- Five number summary:
  - (min, Q1, median, Q3, max).
- Outlier: usually, a value more than 1.5 × IQR above Q3 (> Q3 + 1.5 × IQR) or below Q1 (< Q1 − 1.5 × IQR).
- Boxplot: ends of the box are the quartiles; median is marked; add whiskers, and plot outliers individually.

## Slide 11
### Data Exploration & Pre-processing

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualization.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Data Cleaning.
  - Data Integration.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 12
### Visualization

Visualization is the conversion of data into a visual or tabular format so that the characteristics of the data and the relationship among data items or attributes can be analyzed or reported.

- Visualization of data is one of the most powerful and appealing techniques for data exploration.
  - Humans have a well-developed ability to analyze a large amount of information that is presented visually.
  - Can detect general patterns and trends.
  - Can detect outliers and unusual patterns.

## Slide 13
### Visualizations of Basic Statistical Descriptions

Boxplot: graphic display of five-number summary (another way of displaying the distribution of data).

- Five-number summary of a distribution (Minimum, Q1, Median, Q3, Maximum).
- Data is represented with a box.
  - The ends of the box are at the first and third quartiles, i.e., the height of the box is IQR.
  - The median is marked by a line within the box.
  - Whiskers: two lines outside the box extended to Minimum and Maximum.
  - Outliers: points beyond a specified outlier threshold, plotted individually.

[Figure: Horizontal boxplot on a 0–100 scale in increments of 10. Labels, from left to right: Lower Extreme, Lower Quartile, Median, Upper Quartile, Upper Extreme.]

## Slide 14
### Visualization Techniques: Histograms

- Histogram
  - Usually shows the distribution of values of a single variable.
  - Divide the values into bins and show a bar plot of the number of objects in each bin.
  - The height of each bar indicates the number of objects.
  - Shape of histogram depends on the number of bins.
  - Example: Age Histogram with different number of bins.

[Figure: Two histograms of Age illustrate how changing the number of bins changes the displayed shape; vertical axes show frequency.]

## Slide 15
### Histograms Often Tell More than Boxplots

- The two histograms shown in the left may have the same boxplot representation.
  - The same values for: min, Q1, median, Q3, max (five-number summary).
  - But they have rather different data distributions, from histogram.

[Figure: Two differently shaped histograms beside a common boxplot, demonstrating that the same five-number summary does not uniquely determine a distribution.]

## Slide 16
### Data Exploration & Pre-processing

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualization.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Data Cleaning.
  - Data Integration.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 17
### Similarity and Dissimilarity

- Similarity
  - Numerical measure of how alike two data objects are.
  - Value is higher when objects are more alike.
  - Often falls in the range [0, 1].
- Dissimilarity (e.g., distance)
  - Numerical measure of how different two data objects are.
  - Lower when objects are more alike.
  - Minimum dissimilarity is often 0.
  - Upper limit varies.
- Proximity refers to a similarity or dissimilarity.

## Slide 18
### Data Matrix and Dissimilarity Matrix

- Data matrix
  - $n$ data points with $p$ dimensions.
  - $n\times p$.

$$
X=\begin{bmatrix}
x_{11}&\cdots&x_{1f}&\cdots&x_{1p}\\
\vdots&\vdots&\vdots&\vdots&\vdots\\
x_{i1}&\cdots&x_{if}&\cdots&x_{ip}\\
\vdots&\vdots&\vdots&\vdots&\vdots\\
x_{n1}&\cdots&x_{nf}&\cdots&x_{np}
\end{bmatrix}.
$$

- Dissimilarity matrix
  - $n$ data points, but registers only the distance.
  - A symmetrical matrix.
  - $n\times n$.

$$
D=\begin{bmatrix}
0&&&&\\
d(2,1)&0&&&\\
d(3,1)&d(3,2)&0&&\\
\vdots&\vdots&\vdots&\ddots&\\
d(n,1)&d(n,2)&\cdots&\cdots&0
\end{bmatrix}.
$$

Only the lower triangle is displayed.

## Slide 19
### Dissimilarity between Nominal Variables

- Simple Matching:
  - $m$: # of matches, $p$: total # of variables.

$$d(i,j)=\frac{p-m}{p}.$$

- Example:

| Name | Gender | Fever | Cough | Test-1 | Test-2 | Test-3 | Test-4 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Jack | M | Y | N | P | N | N | N |
| Mary | F | Y | N | P | N | P | N |
| Jim | M | Y | P | N | N | N | N |

$$
d(\mathrm{Jack},\mathrm{Mary})=\frac{2}{7},\qquad
d(\mathrm{Jack},\mathrm{Jim})=\frac{2}{7},\qquad
d(\mathrm{Mary},\mathrm{Jim})=\frac{4}{7}.
$$

## Slide 20
### Distance on Numeric Data: Minkowski Distance

- Minkowski distance: A popular distance measure.

$$
d(i,j)=\left(|x_{i1}-x_{j1}|^h+|x_{i2}-x_{j2}|^h+\cdots+|x_{ip}-x_{jp}|^h\right)^{1/h}.
$$

Where $i=(x_{i1},x_{i2},\ldots,x_{ip})$ and $j=(x_{j1},x_{j2},\ldots,x_{jp})$ are two $p$-dimensional data objects, and $h$ is the order (the distance defined is also called L-h norm).

- Properties
  - $d(i,j)>0$ if $i\ne j$, and $d(i,i)=0$ (Positive definiteness).
  - $d(i,j)=d(j,i)$ (Symmetry).
  - $d(i,j)\le d(i,k)+d(k,j)$ (Triangle Inequality).
- A distance that satisfies these properties is a metric.

## Slide 21
### Special Cases of Minkowski Distance

- $h=1$: Manhattan (city block, L1 norm) distance.
  - E.g., the Hamming distance considers the number of bits that are different between two binary vectors.

$$d(i,j)=|x_{i1}-x_{j1}|+|x_{i2}-x_{j2}|+\cdots+|x_{ip}-x_{jp}|.$$

- $h=2$: (L2 norm) Euclidean distance.

$$d(i,j)=\sqrt{|x_{i1}-x_{j1}|^2+|x_{i2}-x_{j2}|^2+\cdots+|x_{ip}-x_{jp}|^2}.$$

## Slide 22
### Example: Minkowski Distance

| Point | Attribute 1 | Attribute 2 |
| --- | --- | --- |
| x1 | 1 | 2 |
| x2 | 3 | 5 |
| x3 | 2 | 0 |
| x4 | 4 | 5 |

[Figure: Scatterplot of x1=(1,2), x2=(3,5), x3=(2,0), x4=(4,5). Arrows labeled “Dissimilarity Matrices” lead to the two distance matrices below.]

Manhattan (L1):

| L | x1 | x2 | x3 | x4 |
| --- | --- | --- | --- | --- |
| x1 | 0 | | | |
| x2 | 5 | 0 | | |
| x3 | 3 | 6 | 0 | |
| x4 | 6 | 1 | 7 | 0 |

$$d(i,j)=|x_{i1}-x_{j1}|+|x_{i2}-x_{j2}|+\cdots+|x_{ip}-x_{jp}|.$$

Euclidean (L2):

| L2 | x1 | x2 | x3 | x4 |
| --- | --- | --- | --- | --- |
| x1 | 0 | | | |
| x2 | 3.61 | 0 | | |
| x3 | 2.24 | 5.1 | 0 | |
| x4 | 4.24 | 1 | 5.39 | 0 |

$$d(i,j)=\sqrt{|x_{i1}-x_{j1}|^2+|x_{i2}-x_{j2}|^2+\cdots+|x_{ip}-x_{jp}|^2}.$$

Blank entries correspond to the undisplayed upper triangle.

## Slide 23
### Data Exploration & Pre-processing

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualization.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Data Cleaning.
  - Data Integration.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 24
### Data Quality

- Poor data quality negatively affects many data processing efforts.
- Data mining example: If a classification model for detecting people who are loan risky is built by using poor data.
  - Some credit-worthy candidates are denied loans.
  - More loans are given to individuals that are not eligible.
- Data quality problem:
  - Noise and outliers.
  - Missing values.
  - Duplicate data.
  - Wrong data.

## Slide 25
### Data Exploration & Pre-processing

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualization.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Data Cleaning.
  - Data Integration.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 26
### Data Cleaning

- Data in the Real World Is Dirty: Lots of potentially incorrect data, e.g., instrument faulty, human or computer error, transmission error.
  - Incomplete: lacking attribute values, lacking certain attributes of interest, or containing only aggregate data.
    - E.g., Occupation=“ ” (missing data).
  - Noisy: containing noise, errors, or outliers.
    - E.g., Salary=“−10” (an error), Age=“200” (an error).
  - Inconsistent: containing discrepancies in codes or names, e.g.,
    - Age=“42”, Birthday=“03/07/2010”.
    - Was rating “1, 2, 3”, now rating “A, B, C”.
    - Discrepancy between duplicate records.
  - Intentional (e.g., disguised missing data).
    - Jan. 1 as everyone’s birthday?

## Slide 27
### Incomplete (Missing) Data

- Data is not always available.
  - E.g., many tuples have no recorded value for several attributes, such as customer income in sales data.
- Missing data may be due to
  - Equipment malfunction.
  - Inconsistent with other recorded data and so deleted.
  - Data not entered due to misunderstanding.
  - Certain data may not be considered important at the time of entry.
  - No register history or changes of the data.
- Missing data may need to be inferred.

## Slide 28
### How to Handle Missing Data?

- Ignore the tuple: usually done when class label is missing (when doing classification)—not effective when the % of missing values per attribute varies considerably.
- Fill in the missing value manually: tedious + infeasible?
- Fill in it automatically with
  - A global constant: e.g., “unknown”, a new class?!
  - The attribute mean (e.g. “income” is missing).
  - The attribute mean for all samples belonging to the same class: smarter (e.g. “young”, “middle-aged”, “old”).
  - The most probable value: inference-based such as Bayesian formula or decision tree.

## Slide 29
### Noisy Data

- Noise: random error or variance in a measured variable.
- Incorrect attribute values may be due to
  - Faulty data collection instruments.
  - Data entry problems.
  - Data transmission problems.
  - Technology limitation.
  - Inconsistency in naming convention.
- Other data problems which require data cleaning
  - Duplicate records.
  - Incomplete data.
  - Inconsistent data.

## Slide 30
### How to Handle Noisy Data?

- Binning
  - First sort data and partition into (equal-frequency) bins.
  - Then one can smooth by bin means, smooth by bin median, smooth by bin boundaries, etc.
- Regression (vs Classification, target label: Real Number vs Integer & Category)
  - Smooth by fitting the data into regression functions.
- Clustering (group data into clusters)
  - Detect and remove outliers.
- Combined computer and human inspection
  - Detect suspicious values and check by human (e.g., deal with possible outliers, domain/expert knowledge).

## Slide 31
### Smoothing by Bins

- Binning: Binning methods smooth a sorted data value by consulting its “neighborhood,” that is, the values around it. The sorted values are distributed into a number of “buckets” or bins. Because binning methods consult the neighborhood of values, they perform local smoothing.

This figure illustrates some binning techniques. In this example, the data for price are first sorted and then partitioned into equal-frequency bins of size (depth) 3 (i.e., each bin contains three values).

Sorted data for price (in dollars): 4, 8, 15, 21, 21, 24, 25, 28, 34.

| Bin | Partition into equal-frequency bins | Smoothing by bin means |
| --- | --- | --- |
| Bin 1 | 4, 8, 15 | 9, 9, 9 |
| Bin 2 | 21, 21, 24 | 22, 22, 22 |
| Bin 3 | 25, 28, 34 | 29, 29, 29 |

## Slide 32
### Binning Methods for Data Smoothing

- Sorted data for price (in dollars): 4, 8, 9, 15, 21, 21, 24, 25, 26, 28, 29, 34.
- Partition into equal-frequency (equal-depth) bins:
  - Bin 1: 4, 8, 9, 15.
  - Bin 2: 21, 21, 24, 25.
  - Bin 3: 26, 28, 29, 34.
- Smoothing by bin means:
  - Bin 1: 9, 9, 9, 9.
  - Bin 2: 23, 23, 23, 23.
  - Bin 3: 29, 29, 29, 29.

## Slide 33
### Data Exploration & Pre-processing

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualisation.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Data Cleaning.
  - Data Integration.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 34
### Data Integration

- Data integration (Aggregation):
  - Combines data from multiple sources into a coherent store.
- Schema integration: e.g., A.cust-id ≡ B.cust-#.
  - Integrate metadata from different sources.
- Entity identification problem:
  - Identify real world entities from multiple data sources, e.g., Can Wang = Volcano Wang.
- Detecting and resolving data value conflicts
  - For the same real-world entity, attribute values from different sources are different.
  - Possible reasons: different representations, different scales (e.g., Metric vs. British Imperial units).

## Slide 35
### Handling Redundancy in Data Integration

- Redundant data often occur when integrating multiple databases.
  - Object identification: The same attribute or object may have different names in different databases (e.g. “nappy” and “diaper”).
  - Derivable data: One attribute may be a “derived” attribute in another table (e.g., annual revenue from quarterly revenue).
- Redundant attributes may be able to be detected by correlation analysis and covariance analysis.

## Slide 36
### Data Exploration & Pre-processing

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualization.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Data Cleaning.
  - Data Integration.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 37
### Data Transformation

- A function that maps the entire set of values of a given attribute to a new set of replacement values, so that the resulting mining process may be more efficient or effective.
- Methods
  - Smoothing.
  - Attribute/feature construction.
  - Aggregation.
  - Normalization.
    - Min-max normalization.
    - Z-score normalizations.
  - Discretization.

## Slide 38
### Normalize Numerical Attributes

- Min-max normalization: to $[\mathrm{new\_min}_A,\mathrm{new\_max}_A]$.

$$
v'=\frac{v-\min_A}{\max_A-\min_A}
(\mathrm{new\_max}_A-\mathrm{new\_min}_A)+\mathrm{new\_min}_A.
$$

  - Ex. Let income range $12,000 to $98,000 normalized to [0.0, 1.0]. Then $73,600 is mapped to

$$\frac{73{,}600-12{,}000}{98{,}000-12{,}000}(1.0-0)+0=0.716.$$

- Z-score normalization ($\mu$: mean, $\sigma$: standard deviation):

$$v'=\frac{v-\mu_A}{\sigma_A}.$$

  - Ex. Let $\mu=54{,}000$, $\sigma=16{,}000$. Then

$$\frac{73{,}600-54{,}000}{16{,}000}=1.225.$$

## Slide 39
### Normalize Categorical Attributes

- It is often to see some categorical features, nominal or ordinal:
  - Example: Gender (F and M), country (AUS, USA, CHN, etc.), state (NSW, VIC, QLD, etc.).
- How can we use them if we convert them into integer:
  - Example: Gender: 0 or 1, country: 0, 1, 2, …, state: 0, 1, 2, 3, …
- One-Hot encoding can be used to transform categorical features: binary values in a n-bit vector.

[Figure: State is expanded into an eight-bit vector, with the candidate values aligned to positions as below.]

| Candidate values | NSW | VIC | QLD | WA | SA | TAS | ACT | NT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| State one-hot vector | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |

E.g.: original value of state is 2 (or QLD), then the one-hot encoding is [0,0,1,0,0,0,0,0].

## Slide 40
### Discretization

- Discretization: Divide the range of a continuous attribute into intervals.
  - E.g. to replace the age by interval labels 0–10, 11–20, etc., with conceptual labels youth, adult, senior.
- Interval labels can then be used to replace actual data values, the size of data is thus reduced.
- Typical methods: All the methods can be applied recursively.
  - Binning
    - Top-down split, unsupervised.
  - Histogram analysis
    - Top-down split, unsupervised.
  - Clustering analysis (unsupervised, top-down split or bottom-up merge).
  - Decision-tree analysis (supervised, top-down split).
  - Correlation (e.g., $\chi^2$) analysis (unsupervised, bottom-up merge).

## Slide 41
### Simple Discretization: Binning

- Equal-width (distance) partitioning
  - Divides the range into N intervals of equal size: form uniform grid.
  - If A and B are the lowest and highest values of the attribute, the width of intervals will be: $W=(B-A)/N$, N is the number of bins.
  - The most straightforward, but outliers may dominate presentation.
  - Skewed data is not handled well.
- Equal-depth (frequency) partitioning
  - Divides the range into N intervals, each containing approximately same number of samples.
  - Good data scaling.
  - Managing categorical attributes can be tricky.

## Slide 42
### Data Exploration & Pre-processing

- Data Exploration
  - Data Objects and Attribute Types.
  - Basic Statistical Descriptions of Data.
  - Data Visualisation.
  - Measurements of Data Similarity and Dissimilarity.
- Data Pre-processing
  - Data Quality.
  - Major Tasks in Data Pre-processing.
  - Data Cleaning.
  - Data Integration.
  - Data Reduction.
  - Data Transformation and Data Discretization.
- Summary.

## Slide 43
### Have a question?
