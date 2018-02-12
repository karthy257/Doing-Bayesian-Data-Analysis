Ch 6 Problems: Infer Binomial Probability via Exact Mathematical Analysis
================
Brandon Hoeft
February 11, 2018

-   [Exercise 6.1](#exercise-6.1)
    -   [6.1A A single coin flip](#a-a-single-coin-flip)
    -   [Side Note: Calculate Beta Distribution with Base R](#side-note-calculate-beta-distribution-with-base-r)
    -   [6.1B Use posterior from the last flip as the new prior](#b-use-posterior-from-the-last-flip-as-the-new-prior)
    -   [6.1C Observe a tails on the 3rd flip.](#c-observe-a-tails-on-the-3rd-flip.)
    -   [6.1D Change the order of the observed data](#d-change-the-order-of-the-observed-data)
-   [Exercise 6.2](#exercise-6.2)
-   [Exercise 6.3](#exercise-6.3)
-   [Exercise 6.4](#exercise-6.4)
-   [Exercise 6.5](#exercise-6.5)

Exercise 6.1
------------

This another exercise (similar to Ch. 5) to show that the posterior distribution from successive coin flips is invariant to the ordering of the data observed.

### 6.1A A single coin flip

Start with a prior that expresses some uncertainty that a coin is fair: B(*θ* | 4, 4). This beta distribution expresses a prior of a = 4 heads, b = 4 tails. You flip the coin once, returning heads. **what's the posterior distribution**?

A beta posterior distribution is of the form **B(*θ* | z + a, N - z + b)** where:

-   z: number of observed heads from the data
-   N: total number of trials from the data
-   a: shape parameter 1 of beta distribution (i.e. successes)
-   b: shape parameter 2 of beta distribution (i.e. failures)

Using the `BernBeta` function associated with programs from the book, we get:

``` r
source("/Users/bhoeft/Desktop/temp/DBDA Programs/BernBeta.R")
# a = 4, b = 4 for beta prior; observe 1 head from 1 flip. 
BernBeta(priorBetaAB = c(4, 4), Data = c(1))
```

![](Ch6_Problems_files/figure-markdown_github/unnamed-chunk-1-1.png)

    [1] 5 4

We see that the posterior distribution is of the form **B(*θ* | 5, 4)**. Since we observed only 1 head, the posterior distribution only shifts a little to the right. The Posterior is a compromise between our prior beliefs and a single data point observed.

### Side Note: Calculate Beta Distribution with Base R

Our theta, beta prior, and beta posterior could all be derived using base R function `dbeta`.

``` r
# create a sequence of possible values of parameter theta, our prior beliefs. 
theta <-  seq(0, 1, by = 0.1),
# calculate a PDF of our prior beliefs using the beta distribution. 
beta_prior <- dbeta(theta, shape1 = 4, shape2 = 4),
# Posterior distribution B(theta | z + a, N - z + b)
beta_posterior <- dbeta(theta, shape1 = 4 + 1, shape2 = 1 - 1 + 4)
```

### 6.1B Use posterior from the last flip as the new prior

Here a = 5, and b = 4 as our beta distribution shape parameters. They account for the 1 heads in 1 trial observed in the prior experiment. On this next flip, we also get a head. What's our new posterior distribution?

``` r
# a = 5, b = 4 for beta prior; 1 for observing 1 heads
BernBeta(priorBetaAB = c(5, 4), Data = c(1))
```

![](Ch6_Problems_files/figure-markdown_github/unnamed-chunk-3-1.png)

    [1] 6 4

We see that the posterior distribution is of the form **B(*θ* | 6, 4)**.

### 6.1C Observe a tails on the 3rd flip.

Using the posterior from the last flip (accounts for 2 heads in 2 flips per the data), make a third coin flip, which returned tails. Now, what is the new posterior?

``` r
# a = 6, b = 4 for beta prior; 1 for observing 1 heads
BernBeta(priorBetaAB = c(6, 4), Data = c(0))
```

![](Ch6_Problems_files/figure-markdown_github/unnamed-chunk-4-1.png)

    [1] 6 5

We see that the posterior distribution is of the form **B(*θ* | 6, 5)**.

### 6.1D Change the order of the observed data

If you changed the order of the observed flips from **Head**, **Head**, **Tail** to **Tail**, **Head**, **Head** instead, would we get the same posterior distribution as observed in **6.1C**? Yes, because this analysis assumes each observation is treated as an independent event.

``` r
# Data observed previously is T, H. So B(theta | 1 + 4, 2 - 1 + 4) -> B(theta | 5, 5) is new prior
# toss a Head on final toss
BernBeta(priorBetaAB = c(5, 5), Data = c(1))
```

![](Ch6_Problems_files/figure-markdown_github/unnamed-chunk-5-1.png)

    [1] 6 5

We get the same final posterior form as before regardless of ordering of the 3 coin tosses. The posterior distribution is of the identical form **B(*θ* | 6, 5)** from **6.1C**.

Exercise 6.2
------------

Exercise 6.3
------------

Exercise 6.4
------------

Exercise 6.5
------------