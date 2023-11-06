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

      .. math::
         G: (Z, X, Y^*) \to Y^ = (Y_1^, \ldots, Y_K^).  \text{(The Imputation Step)}

   2. For each l=1, ..., L:

      a. Randomly generate Z^(l) according to the randomization design P.

      b. Obtain full imputed outcomes Y^(l) based on (Z^(l), X, Y*):

         .. math::
            G: (Z^{(l)}, X, Y^*) \to Y^{(l)} = (Y_1^{(l)}, \ldots, Y_K^{(l)}). \text{(The Re-Imputation Step)}

      c. Calculate T^(l) = T(Z, Y^(l)) for the l-th re-imputation run.

   3. Approximate the finite-population-exact p-value under Fisher's sharp null H0:

      .. math::
         \hat{p} = \frac{1}{L} \sum_{l=1}^{L} \mathbf{1}\{T^{(l)} \geq t\}.

   Output:
   - Approximate finite-population-exact p-value \(\hat{p}\) under Fisher's sharp null H0.

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

   2. Use (X, Y^) and outcome prediction model H to get predicted outcomes \(\tilde{Y}\) (Covariate Adjustment after Imputation).

   3. Calculate \(t = T(Z, \varepsilon)\), where \(\varepsilon = Y^ - \tilde{Y}\) is the residuals vector.

   4. For each \(l = 1, \ldots, L\):

      a. Randomly generate \(Z^{(l)}\) according to randomization design P.

      b. Obtain full imputed outcomes \(Y^{(l)}\) based on \((Z^{(l)}, X, Y^*)\) and algorithm G.

      c. Use \((X, Y^{(l)})\) and model H to get predicted outcomes \(\tilde{Y}^{(l)}\) (Covariate Adjustment after Re-Imputation).

      d. Calculate \(T^{(l)} = T(Z, \varepsilon^{(l)})\) and store the value, where \(\varepsilon^{(l)} = Y^{(l)} - \tilde{Y}^{(l)}\) is the residuals vector for the l-th permutation.

   5. Approximate the finite-population-exact p-value under Fisher's sharp null H0 via:

      .. math::
         \hat{p}_{\text{adj}} = \frac{1}{L} \sum_{l=1}^{L} \mathbf{1}\{T^{(l)} \geq t\}.

   Output:
   - Approximate finite-population-exact p-value \(\hat{p}_{\text{adj}}
