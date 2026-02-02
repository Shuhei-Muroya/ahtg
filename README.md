
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
library(MASS)
# Prepare data (Generate dummy data)
set.seed(1)
N <- 1500
p <- 800
rho <- 0.5
Sigma <- matrix(rho, nrow = p, ncol = p)
diag(Sigma) <- 1
Sigma <- outer(1:p, 1:p, function(i, j) ifelse(i == j, 1, rho))

X <- mvrnorm(n = N, mu = rep(0, p), Sigma = Sigma)
beta_true <- c(rep(1, p/2), rep(0, p/2))
y <- X %*% beta_true + rnorm(N)

## Automatically select the hyperparameters and compute the lasso
result<-auto_lasso(X, y, T_hope=20)

## Check the estimated coefficients
print(result$coefficients)

## Check the Pareto front and the tuned configuration (if glmnet was used)
print(result$Pareto_front)
print(result$hyperparameters)

```

