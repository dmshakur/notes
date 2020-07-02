
# Introduction To Data Mining

## Basic vocabulary
### What is data
A collection of objects defined by attributes

Attributes are essentially columns, and objects are essentially rows.

## Attributes
### Attribute values
Each attribute has a set of values objects draw from. 
\The same attribute can be mapped to different attribute values.

The people who create the dataset determine how the attributes are measured or formatted.

### Attribute classification
* Discrete attributes: Has a finite or countable infinite set of values.
* Continuous attributes: Has real numbers as attribute values.

Categorical:
* Nominal: Id numbers, eye color, zip codes
* Ordinal: Rankings, grades, clothing sizes
Numerical:
* Interval: Numbers with a true zero
* Ratio: Numbers with no true zero

## Basic data types
### Types of datasets
* Record:
  * Data matrix
  * Document data
  * Transaction data
* Graph
  * The internet
  * Molecular structures
* Ordered
  * Spatial data
  * Temporal data
  * Sequential data
  * Genetic sequence data

### Record data
Data the consists of a collection of records, each of which consists of a fixed set of attributes.

### Data matrix
Data objects with only numeric attributes can be represented by an $m\times n$ matrix, where there are $m$ rows, one for each object, and $n$ columns, one for each attribute. Attributes can be thought of as points in a graph.

### Document data
Each document becomes a "term" vector.
Each term is a component (attribute) of the vector.

### Transaction data
A special type of record data where each record (transaction) involves a set of items.

### Graph data
A graph where the vertices represent nodes of data, and lines represent some kind of connection.

### Ordered data
Example, genomic sequence data, spatial, and temporal data.
\Time series data is the most common type of ordered data.

## Data quality
One of the most commonly overlooked, and skipped part of data science. 

There are three very important data quality questions we need to ask ourselves.
* What problems should we worry about?
* How can we detect problems with the data?
* What can we do about these problems?
Ask yourself these questions early on when you look at a data set.

## Data noise
Noise can happen with human inconsistency of labeling.

Noise is fundamentally invalid data points.

### Outliers
Data objects with characteristics that are considerably different than most of the other objects in the data set.

### Missing values
Reasons for missing values
* Information not collected: People declining to give their age and weight.
* Attributes may not be applicable to all cases.

Handling missing values
* Eliminate data.
* Estimate missing values, mean, mode, etc.
* Ignore the missing value during analysis.
* Replace with all possible values (weighted by their probabilities).

### Duplicate data
Data set may include data objects that are duplicates, or almost duplicates, of one another.

Major issue when merging data from heterogeneous sources.

With heterogeneous data be careful with filtering out duplicate data objects.

Heterogeneous data are any data with high variability of data types and formats. They are possibly ambiguous and low quality due to missing values, high data redundancy, and untruthfulness. It is difficult to integrate heterogeneous data to meet the business information demands.

## Data cleaning
Data cleaning is a subset of preprocessing.

Data preprocessing types, there is some overlap between these.
* Aggregation
* Sampling
* Dimensionality reduction
* Feature subset selection
* Feature creation
* Discretization and binarization
* Attribute transformation

### Aggregation
Combining two or more attributes into a single attribute, or object(s).

Purpose
* Data reduction, reduce the amount of data.
* Change of scale.
* 
* More stable data, for less variety, reducing random noise.

Aggregated data tends to reduce random noise.

### Sampling
The main technique used for data selection. Data miners sample because processing the entire set of data of interest is too expensive or time consuming.

The key principle for effective sampling is: A sample will work almost as well as using the entire data set if the sample is representative.

### Types of sampling
* Simple random sampling: There is a equal probability of selecting any particular item.
* Stratified sampling. Split the data into several partitions, draw random samples from each partition.
* Sampling without replacement: As each item is selected, it is removed from the population.
* Sampling with replacement: Objects are not removed from the population as they are selected for the sample.

### Dimensionality reduction
The curse of dimensionality:
\When dimensionality increases, data becomes increasingly sparse in the space that it occupies.
\Definitions of density and distance between points, which is critical for clustering and outlier detection, become less meaningful.

If you have enough dimensions everything looks like an outlier.

Purpose:
* Avoid curse of dimensionality
* Reduce tiem and memory required.
* Allow data to be more easily visualized.
* May help to eliminate irrelevant features or reduce noise.
Techniques:
* PCA
* Singular value decomposition

### Feature subset reduction
Another way to reduce dimensionality of data

Redundant features:
\Two very similar features that are almost the same thing.
\Irrelevant features:
\A student's ID number is often irrelevant to the task of predicting students' GPA.

#### Techniques
* Brute-force approach: Try all possible feature subsets as input to data mining algorithm.
* Embedded approach: Feature selection occurs naturally as part of the data mining algorithm.
* Filter approach: Features are selected before data mining algorithm is run.
* Wrapper approach: Use a data mining algorithm as a black box to find the best subset of attributes.

### Feature creation
Original attributes not always best representation of information; create new features which are more efficient/focused.

#### Three general methodologies
* Feature extraction
* Feature construction
* Mapping data to new space
    * Fourier transform
    * Wavelet transform

### Attribute transformation
A function that maps the entire set of values of a given attribute to a new set of replacement values such that each old value can be identified with one of the new values.
\i.e. standardization and normalization

Standardization is where we take the numerical data and we subtract the mean and divide by the standard deviation. It forces the data to have a mean of 0 and a standard deviation of 1.

Normalization is where we subtract the minimum from every data point and divide by the maximum, this puts everything in the range of 0 to 1. It does distort the data to a certain extent.

## Similarity and dissimilarity
Similarity:
* Numerical measure of how alike two data objects are.
* Is higher when objects are more alike.
* Often falls between the range of 0 and 1.
Dissimilarity:
* Numerical measure of how different are two data objects..
* Lower when objects are more alike.
* Minimum dissimilarity is often 0.
* Upper limit varies.

Proximity refers to either how similar or dissimilar.

### Euclidean distance
Equation
$$
dist=\sqrt{\sum_{k=1}^{n}(p_k-q_k)^2}
$$
$n$ is the number of dimensions.
$p_k$ and $q_k$ are, respectively, the $k^{th}$ attributes of data objects $p$ and $q$.

### Cosine similarity
Turn documents into term vectors, and you can find the similarity between them. 

You take the dot product of the term vectors, and divide by the product of the magnitudes.

Good for documents, gives a clean 0 to 1 measurement and suffers less from the curse of dimensionality.

### Correlation
Measures the linear relationship between objects

Standardize data objects ($p$ and $q$) and then take their dot product.

$p'_k=\frac{p_k-mean(p)}{stddev(p)}$

$q'_k=\frac{q_k-mean(q)}{stddev(q)}$

$correlation(p,q)=p'q'$

Often used as a metric to evaluate regression models.

## Data exploration and visualization
* Visualization and calculation to better understand the characteristics of data.
* Key motivations of data exploration.
  * Helping to select the right tool for preprocessing or analysis.
  * Making use of humans' abilities to recognize patterns.
    * People can recognize patterns not captured by data analysis tools.

### Summary statistics
Examples:
* Frequency
* Mean
* Standard deviation

### Measures of center: Mean and median
The mean is very sensitive to outliers. The median is the 50% value.

### Measures of spread: Range and variance
* Range is the difference between maximum and minimum
* Variance and standard deviation are the most common measures of spread between points.

