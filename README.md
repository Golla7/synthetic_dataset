# synthetic_dataset
onditional and marginal effects (conditional_marginal)

This folder contains example code for the "conditional and marginal treatment effect" lecture of the short course.

In this repo, we implemented the following approaches:

Conditional treatment effect point estimate and SE using Huber-White robust “sandwich” estimator

Marginal treatment effect point estimate using standardization

SE of marginal treatment effect using

Nonparametric bootstrap method (Efron and Tibshirani, 1994)
Delta method
Parametric bootstrap method (Aalen et al., 1998)
How to run the scripts

The utilized functions to calculated the conditional and marginal estimates are in conditional_marginal/funs/funs.R. A wrapper function summary_Estimate could be used to obtain the conditional and marginal estimates with corresponding SE calculated in different ways. It can be called by summary_Estimate(data=data, formula = as.formula("y ~ trt + X1"), nsim = 1000, trt.var = "trt", type = "OR"), where

data is the data frame including treatment factor and covariates of used samples

formula specifies the response, treatment variable and adjusted covariates

nsim is the number of bootstrap replicates when calculating SE for marginal estimate

trt.var is the name of treatment variable

type is the used estimator, "OR" for odds ratio and "RD" for risk difference.

To run the demo, first run source("conditional_marginal/src/01_gen_data.R"), which will generate the toy dataset using benchtm package. The toy dataset has 500 samples randomised to pbo (0) or treatment (1) arm with 10 covariates. And the response is generated using logit(p) = 0.5*(X1=='Y') + 1*X3 + 0.3*trt. Therefore, there are two prognostic covariates, X1 and X3.

Then source("conditional_marginal/src/02_analysis.R") gives the conditional and marginal estimates. And here we compare

unadjusted, Y ~ trt

adjusted with one moderate prognostic factor Y ~ trt + X1

adjusted with one moderate and one strong prognostic factor Y ~ trt + X1 + X3

adjusted with both prognostic factors and an unrelated factor Y ~ trt + X1 + X3 + X8

Both odds ratio and risk difference estimates will be calculated and saved in conditional_marginal/output/Result_condi_margin_OR.csv and conditional_marginal/output/Result_condi_margin_RD.csv respectively.
