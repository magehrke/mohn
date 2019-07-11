---
tags: []
title: Chapter 2
sub_heading: 'Probability Distributions'
banner_image: '/uploads/books.jpg'
publish_date: '2019-07-01T03:00:00.000+00:00'
order_number: 2

---

#### Density Estimation
#### Parametric Distributions
* Examples: Gaussian, Multinomial Distribution

#### Conjugate Priors
#### Nonparametric Distributions
* Examples: Histograms, Nearest-Neighbours, Kernels


## 2.1 Binary Variables
#### Bernoulli distribution:
* Probability for a binary variable.
* $\text{Bern}(x|\mu) = \mu^x(1-\mu)^{1-x}$
* Normalized
* Mean: $\text{E}[x] = \mu$
* Variance: $\text{var}[x] = \mu(1-\mu)$
* Likelihood: $p(D|\mu) = \prod_{n=1}^{N}p(x_n|\mu)
  = \prod_{n=1}^{N}\mu^{x_n} (1-\mu)^{1-x_n}$
* log Likelihood: $\ln p(D|\mu) = \sum_{n=1}^{N}p(x_n|\mu)
  = \sum_{n=1}^{N} x_n  \ln\mu + (1-x_n) \ln (1-\mu)$
* ML solution: sample mean, which can be written as $\mu_{ML} = \dfrac{1}{N}$ if
  $m$ is the amount of $x = 1$.

#### Sample Mean:
* $\mu = \dfrac{1}{N}\sum_{n=1}^N x_n$

#### Binomial distribution:
* Probability that a binary variable is $m$ times $x = 1$.
* Binomial distribution is proportional to Binomial Likelihood.
* $\text{Bin}(m|N, \mu) = \binom{N}{m} \mu^m (1 - \mu)^{N-m} ~ \text{where} ~
\binom{N}{m} \equiv \dfrac{N!}{(N-m)!m!}$

### 2.1.1 The beta distribution



## 2.5 Nonparametric Methods

#### Introduction:
* Nonparametric approaches to density estimation make few assumptions about the
form of the distribution.
* The following methods are frequentist methods, however nonparametric Bayesian
methods attract increasing interest.

#### Histograms:
* Single continuous variable
* Partition x into distinct bins of with $\Delta_i$
* Count the number $n_i$ of observations of $x$ falling in bin $i$.
* Probability: $p_i = \dfrac{n_i}{N\Delta_i}$
* Most of the time all $\Delta_i$ have the same width ($\Delta_i = \Delta$).
* If $\Delta$ is very small, the resulting density model is very spiky with
lots of structure which is not present in the underlying distribution.
* If $\Delta$ is too large, the result is too smooth.
* In principle, histograms depend on the choice of edge location, though this
is less significant than the value of $\Delta$.
* Once the histogram has been computed, the data can be discarded (unlike the
  other two methods)
  * Good if data set is too large or the data arrives sequentially.
* In practice, histograms are used for quick visualizations in 1D or 2D.
  * Unsuited to most density estimation applications.
  * Discontinuities at bin edges
  * Curse of dimensionality: If we divide each variable in a D-dimensional
  space into M bins, the total number of bins will be $M^D$.


#### Lessons from histograms:

* To estimate probability densities at a specific location, we should consider
the data points that lie within some local neighbourhood of that.
  * Concept of locality needs some form of distance measure (e.g. Euclidean).
  * Spacial extend of the local region is a natural smoothing parameter.

* The value of the smoothing parameter should be neither too small or too large.


### 2.5.1 Kernel Density Estimators

#### Assumptions:
* Unknown density p(x) in some D-dimensional space
* Euclidean distance
* region R containing x
* N collected observations

#### Probability mass:
* Probability mass associated with region R is given by
$P = \int_R p(\textbf{x}) \text{d}\textbf{x}$


#### Density estimate:



\[ p(\textbf{x}) = \dfrac{K}{NV}\]

* This depends on two assumptions: (a) the region $R$ is sufficiently small that
the density is appoximately constant over the region and (b) sufficiently large
that the number $K$ of points falling inside the region is sufficient for the
binomial distribution to be sharply peaked.


#### Kernel density estimator:
* (also called Parzen estimator).
* The class of density model given by:
\[p(\textbf{x}) = \dfrac{1}{N} \sum_{n=1}^N \dfrac{1}{h^D} k \left(\dfrac{\textbf{x} - \textbf{x}_n}{h}\right)\]


#### Choice of Kernels:
* We can choose any kernel function $k(\mathbf{u})$ that satisfies
$k(\mathbf{u}) \ge 0$ and $\int k(\mathbf{u}) \text{d}\textbf{u} = 1$.
  * This ensures that the resulting probability dist is nonnegative and integrates
to one.
* No computation involved in the training phase, this simply requires storage!
* However, this is also one of its great weaknesses; the computational cost of
evaluating the density grows linearly with the siye of the data set.
