R-package
=====

.. _installation:

Installation
------------

To use iArt in R, install it using the devtools package:

.. code-block:: R

   # Install iArt from GitHub
   devtools::install_github("Imputation-Assisted-Randomization-Tests/iArt")

Conducting Randomization Tests with iArt
-----------------------------------------

The `iArt.test` function in the iArt package allows for conducting finite-population-exact randomization tests in design-based causal studies with missing outcomes. 


Basic Usage Example
--------------------

To perform a basic randomization test in R:

.. code-block:: R

    library(iArt)

    Z <- c(1, 1, 1, 1, 0, 0, 0, 0)

    X <- matrix(c(5.1, 3.5, 4.9, NA, 4.7, 3.2, 4.5, NA, 7.2, 2.3, 8.6, 3.1, 6.0, 3.6, 8.4, 3.9), ncol = 2)

    Y <- matrix(c(4.4, 0.5, 4.3, 0.7, 4.1, NA, 5.0, 0.4, 1.7, 0.1, NA, 0.2, 1.4, NA, 1.7, 0.4), ncol = 2)
    
    result <- iArt.test(Z, X, Y, L = 1000, verbose = TRUE)

    print(result)

Different Imputation Methods in iArt
--------------------------------------

The iArt package supports various methods for imputing missing data in R. Each method can be specified using the `G` parameter in the `iArt.test` function. It is slightly different from the Python version, because the R version uses the missforest and mice, whereas the Python version uses the IterativeImputer

To specify an imputation method in R, set the `G` parameter in the `iArt.test` function to one of the options. 

- **MICE (`'mice'`)**: 
    Multiple Imputation by Chained Equations (MICE) is a popular imputation method in R. It is a fully conditional specification method that creates multiple imputations by filling in missing data multiple times using a specified imputation model.

    .. code-block:: R

        result <- iArt.test(Z, X, Y, G = 'mice', L = 1000, verbose = TRUE)

    You can find more about the `mice` package on its CRAN page here: `mice <https://CRAN.R-project.org/package=mice>`_.

- **MissForest (`'missforest'`)**:
    MissForest is a non-parametric imputation method in R. It is a non-parametric imputation method that uses a random forest to impute missing data.

    .. code-block:: R

        result <- iArt.test(Z, X, Y, G = 'missforest', L = 1000, verbose = TRUE)

    For more information on `missforest`, visit the CRAN page: `missforest <https://CRAN.R-project.org/package=missForest>`_.

Handling Strata in the Data
---------------------------

Incorporate strata into your analysis in R using the `S` parameter in the `iArt.test` function. All strata should be in ascending order, and the stratum index for each data point should be specified in the same order as the data points

.. code-block:: R

    # S vector indicates the stratum index for each data point
    S <- c(0, 0, 1, 1, 1, 2, 2, 2)
    
    # Incorporating strata into the analysis
    result <- iArt.test(Z, X, Y, S = S, L = 1000, verbose = TRUE)

Covariate Adjustment 
--------------------

Enable covariate adjustment in R by setting the `covariate_adjustment` parameter to `TRUE` in the `iArt.test` function. This will use linear regression to adjust for covariates in the analysis.

.. code-block:: R

    # Conducting a randomization test with covariate adjustment
    result <- iArt.test(Z, X, Y, covariate_adjustment = TRUE, L = 1000, verbose = TRUE)

Specifying an Alternative Hypothesis:
-------------------------------------

To specify an alternative hypothesis in R, set the `alternative` parameter in the `iArt.test` function to either `'greater'`, `'less'`, or `'two-sided'`.

.. code-block:: R

    # For a one-sided test greater than
    result <- iArt.test(Z, X, Y, alternative = "greater", L = 1000, verbose = TRUE)

    # For a one-sided test less than
    result <- iArt.test(Z, X, Y, alternative = "less", L = 1000, verbose = TRUE)

    # For a two-sided test
    result <- iArt.test(Z, X, Y, alternative = "two-sided", L = 1000, verbose = TRUE)

Setting a Random State for Reproducibility:
-------------------------------------------

Set a random state for reproducibility in R:


.. code-block:: R

    # Setting a seed for reproducibility
    set.seed(42)
    result <- iArt.test(Z, X, Y, L = 1000, verbose = TRUE)