Algorithms in I-ART
===================

The I-ART package implements several algorithms for conducting finite-population-exact randomization tests in the context of design-based causal studies with missing outcomes. Below are the two primary algorithms used in I-ART.

Algorithm: Imputation and Re-Imputation Framework
-------------------------------------------------

This algorithm forms the core of I-ART for testing Fisher's sharp null hypothesis under the presence of missing outcome data.

.. code-block:: none

   Algorithm: An "imputation and re-imputation" framework for testing Fisher's sharp null.
   ---------------------------------------------------------------------------------------
   
   Input:
   - Prespecified number of monte-carlo re-imputation runs L (e.g., L=10,000).
   - Observed treatment indicators Z, observed covariates X, and observed outcomes with missingness Y* for K outcomes.
   - Y* contains all observed missingness status information M.

   Steps:
   1. Use (Z, X, Y*) and a chosen algorithm G to obtain full imputed outcomes Y^:
      G: (Z, X, Y*) -> Y^ = (Y_1^, ..., Y_K^).  (The Imputation Step)

   2. For each l=1, ..., L:
      a. Randomly generate Z^(l) according to the randomization design P.
      b. Obtain full imputed outcomes Y^(l) based on (Z^(l), X, Y*):
         G: (Z^(l), X, Y*) -> Y^(l) = (Y_1^(l), ..., Y_K^(l)). (The Re-Imputation Step)
      c. Calculate T^(l) = T(Z, Y^(l)) for the l-th re-imputation run.

   3. Approximate the finite-population-exact p-value under Fisher's sharp null H0:
      p^ = (1/L) ∑ (l=1 to L) 1{T^(l) >= t}.

   Output:
   - Approximate finite-population-exact p-value p^ under Fisher's sharp null H0.

Algorithm: Imputation and Re-Imputation with Covariate Adjustment
----------------------------------------------------------------

This variant of the algorithm includes an additional step of covariate adjustment after the imputation process.

.. code-block:: none

   Algorithm: An "imputation and re-imputation" framework with covariate adjustment.
   ----------------------------------------------------------------------------------
   
   Input:
   - Prespecified number of monte-carlo re-imputation runs L (e.g., L=10,000).
   - Observed treatment indicators Z, observed covariates X, and observed outcomes with missingness Y* for K outcomes.
   - Y* contains all observed missingness status information M.

   Steps:
   1. Use (Z, X, Y*) and chosen imputation algorithm G to obtain full imputed outcomes Y^.
   2. Use (X, Y^) and outcome prediction model H to get predicted outcomes Y~ (Covariate Adjustment after Imputation).
   3. Calculate t=T(Z, ε), where ε=Y^ - Y~ is the residuals vector.
   4. For each l=1, ..., L:
      a. Randomly generate Z^(l) according to randomization design P.
      b. Obtain full imputed outcomes Y^(l) based on (Z^(l), X, Y*) and algorithm G.
      c. Use (X, Y^(l)) and model H to get predicted outcomes Y~(l) (Covariate Adjustment after Re-Imputation).
      d. Calculate T^(l)=T(Z, ε^(l)) and store the value, where ε^(l)=Y^(l) - Y~(l) is the residuals vector for the l-th permutation.
   5. Approximate the finite-population-exact p-value under Fisher's sharp null H0 via: p^_adj = (1/L) ∑ 1{T^(l) >= t}.

   Output:
   - Approximate finite-population-exact p-value p^_adj under Fisher's sharp null H0.
