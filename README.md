
# ahtg

<!-- badges: start -->
<!-- badges: end -->

The ahtg package automatically provides appropriate hyperparameters for glmnet function.
It selects the appropriate hyperparameters for glmnet based on the given data.
Additionally, it can compare lars and glmnet in terms of computation time and choose the better package for the task.

## Installation

You can install the development version of ahtg from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
library(devtools)
devtools::install_github("Shuhei-Muroya/ahtg")
```
or
``` r
remotes::install_github("Shuhei-Muroya/ahtg")
```

## Example

This is a basic example :

``` r
library(ahtg)

# Prepare data (Generate dummy data)
set.seed(1)
N <- 1500
p <- 800
X <- matrix(rnorm(N * p), N, p)
# True coefficients (Only first 10 variables are active)
beta_true <- c(rep(2, 10), rep(0, p - 10))
# Response (Signal + Noise)
y <- X %*% beta_true + rnorm(N)

## Automatically select the hyperparameters and compute the lasso
result<-auto_lasso(X, y, T_hope=20)

## Check the estimated coefficients
print(result$coefficients)

## Check the Pareto front and the tuned configuration (if glmnet was used)
print(result$Pareto_front)
print(result$hyperparameters)
```

