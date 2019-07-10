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
* ML solution: sample mean, which can be written as $\mu_{ML} = m/N$ if $m$ is
  the number of $x = 1$.

#### Sample Mean:
* $\mu = \dfrac{1}{N}\sum_{n=1}^N x_n$

#### Binomial distribution:
* Probability that a binary variable is $m$ times $x = 1$.
* Binomial distribution is proportional to Binomial Likelihood.
* $\text{Bin}(m|N, \mu)$ =

### 2.1.1 The beta distribution
