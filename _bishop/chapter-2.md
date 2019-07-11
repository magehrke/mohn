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
* a function that gives the probability that a discrete random variable is
exactly equal to some value.
* It differs from a probability density function
in that the latter is associated with continuous rather than discrete random
variables; the values of the probability density function are not probabilities
as such: a PDF must be integrated over an interval to yield a probability.


* Probability mass associated with region $R$ is given by
$P = \int_R p(\textbf{x}) \text{d}\textbf{x}$

* Because each data point has probability $P$ of falling within $R$, the total
number $K$ of points that lie inside $R$ will be distributed according to the
binomial distribution:
$\text{Bin}(K|N, P) = \dfrac{N!}{(N-K)!K!} P^K (1 - P)^{N-K}$

* Mean Fraction of points that fall into the region: $E[K/N] = P$
* Variance: $\text{var}[K/N] = P(1-P)/N$
#### Density estimate:

* For large N this distribution with be sharply peaked around the mean and so
\[K \approx NP\]
* If the region $R$ is sufficiently small that the probability density $p(x)$
is roughly constant over the region, then we have
\[P \approx p(\textbf{x})V\]
* With this we obtain our density estimate:



\[ p(\textbf{x}) = \dfrac{K}{NV}\]

* This depends on two assumptions: (a) the region $R$ is sufficiently small that
the density is appoximately constant over the region and (b) sufficiently large
that the number $K$ of points falling inside the region is sufficient for the
binomial distribution to be sharply peaked.

#### 2 ways to estimate the density:
* Fix $K$ and determine $V$ from the data = $K$-nearest-neighbours
* Fix $V$ and determine $K$ from the data = kernel density estimator
* Both converge to the true probability, if $V$ shrinks with N and $K$ grows
with N

#### Kernel density estimator:
* Simple kernel function (here also called Parzen window) with a unit cube
centered around the origin:
\[k(\textbf{u}) =     
\begin{cases}
      1, & \text{if}\ |u_i| \le 1/2, i = 1, \dots , D \\
      0, & \text{otherwise}
\end{cases}\]

* The total number of data points lying insida a cube of side $h$ is:
\[K = \sum_{n=1}^N k \left(\dfrac{\textbf{x} - \textbf{x}_n}{h}\right)\]


* Now, a kernel density estimator (also called Parzen estimator) is the class of
density models given by:
\[p(\textbf{x}) = \dfrac{1}{N} \sum_{n=1}^N \dfrac{1}{h^D} k
\left(\dfrac{\textbf{x} - \textbf{x}_n}{h}\right)\]

* We have used $V = h^D$
* No computation involved in the training phase, this simply requires storage!
* However, this is also one of its great weaknesses; the computational cost of
evaluating the density grows linearly with the size of the data set.
* This estimator will suffer from discontinuities at the boundaries of the cubes

#### Guassian kernel density estimator:
* We can obtain a smoother kernel function, if we chose a Gaussian kernel

\[p(\textbf{x}) = \dfrac{1}{N} \sum_{n=1}^N \dfrac{1}{(2\pi h^2)^{D/2}} \exp
\left\{\dfrac{||\textbf{x} - \textbf{x}_n||^2}{2h^2}\right\}\]

* where $h$ represents the standard deviation of the Gaussian component.
* Like with histograms, our hyperparameter ($h$ in this case) is a smoothing
parameter.
* The optimization of $h$ is a problem of model complexity analogous to the
choice of bin width or degree of polynomial.

#### Choice of Kernels:
* We can choose any kernel function $k(\mathbf{u})$ that satisfies
$k(\mathbf{u}) \ge 0$ and $\int k(\mathbf{u}) \text{d}\textbf{u} = 1$.
* This ensures that the resulting probability dist is nonnegative and integrates
to one.

### 2.5.2 Nearest-neighbour methods

#### K-nearest-neighbour:
* One of the difficulties of kernel methods is that the parameter $h$ is fixed
for all kernels / data points. Depending on how many points lie in a region,
$h$ might be perfectly chosen for some location and poorly for others.
* We can fix this in NN by choosing a fixed $K$ and determining $V$.
* We consider a small sphere centered on the point x and allow the radius to
grow until it contains precisely $K$ data points.
* The estimate is then given by $p(\textbf{x}) = {K}/{NV}$ with $V$ set to the
volume of the resulting sphere.
* Now the parameter $K$ governs the degree of smoothing
* Again, K should neither be too large nor too small.
* The model produced by K-NN is not a true density model.

#### K-NN for classification:
* Apply K-NN seperately for each class and make use of Bayes' theorem.
* Assume a data set with $N_k$ points in class $C_k$ with N points in total
* If we with to classify a new point x, we draw a sphere around x  containing
precisely K points irrespective their class.
* Suppose this squere has volume $V$ and contains $K_k$ points from class $C_k$.
</br></br>
* The density associated with each class:
\[p(\textbf{x}|C_k) = \dfrac{K_k}{N_kV}\]
* The unconditional density:
\[p(\textbf{x}) = \dfrac{K}{NV}\]
* The class priors:
\[p(C_k) = \dfrac{N_k}{N}\]
* The posterior:
\[p(C_k|\textbf{x}) = \dfrac{p(\textbf{x}|C_k)p(C_k)}
{p(\textbf{x})} = \dfrac{K_k}{K}\]

* Minimizing the misclassification probability is done by assigning x to the
class having the largest posterior probability.

#### The nearest neighbour rule:
* K = 1
* An unseen point is simply assigned to the nearest point from the training set.
* In the limit $N \rightarrow \infty$ the error rate is never more than twice
the minimum achievable error rate of an optimal classifier.

#### Sum up nonparametric models:
* Both K-NN and kernel density estimator need the entire training data set to be
stored, leading to expensive computation if the data set is large.
* Tree-based search structures allow finding neighbours efficiently
* Nevertheless, nonparametric methods are still severly limited
* However, we have seen that simple parametric models are very restricted in
terms of the forms of distribution that they can represent
</br></br>
* We need to find density models that are very flexible and yet for which the
complexity of the models can be  controlled independently of the training
set size
