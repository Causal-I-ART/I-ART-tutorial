Python-package
=====

.. _installation:

Installation
------------

To use iArt, install it using pip:

.. code-block:: console

   (.venv) $ pip install python-iArt

Conducting Randomization Tests with iArt
-----------------------------------------

The `test` function in the iArt package allows for conducting finite-population-exact randomization tests in design-based causal studies with missing outcomes. 

.. autofunction:: iArt.test

Basic Usage Example
--------------------

To perform a basic randomization test:

.. code-block:: python

    import numpy as np
    import iArt

    Z = np.array([1, 1, 1, 1, 0, 0, 0, 0])

    X = np.array([[5.1, 3.5], [4.9, np.nan], [4.7, 3.2], [4.5, np.nan], [7.2, 2.3], [8.6, 3.1], [6.0, 3.6], [8.4, 3.9]])

    Y = np.array([[4.4, 0.5], [4.3, 0.7], [4.1, np.nan], [5.0, 0.4], [1.7, 0.1], [np.nan, 0.2], [1.4, np.nan], [1.7, 0.4]])
    
    result = iArt.test(Z=Z, X=X, Y=Y, L=1000, verbose=True)

Different Imputation Methods in iArt
--------------------------------------

The iArt package supports various methods for imputing missing data. Each method can be specified using the `G` parameter in the `iArt.test` function. Below are descriptions of each imputation method:

- **XGBoost (`'xgboost'`)**: 
  Utilizes the XGBoost algorithm, which is effective for complex datasets with nonlinear relationships. This method is suitable when the dataset has complex patterns that simpler methods might not capture well.

- **Bayesian Ridge (`'bayesianridge'`)**: 
  Employs Bayesian Ridge Regression, a linear model that is useful for datasets where a linear relationship is expected between the features and the outcome.

- **Median (`'median'`)**: 
  Imputes missing values using the median of each feature. This method is robust to outliers and is a good choice for skewed data.

- **Mean (`'mean'`)**: 
  Uses the mean of each feature for imputation. This method is best used when the data is normally distributed and there are no significant outliers.

- **LightGBM (`'lightgbm'`)**: 
  Applies the LightGBM algorithm, which is efficient for large datasets and can handle categorical features well. It's an appropriate choice for datasets with complex patterns and a mix of feature types.

- **MICE (`'mice'`)**: 
  Stands for Multiple Imputation by Chained Equations. It's a sophisticated method that models each feature with missing values as a function of other features in a round-robin fashion. Suitable for datasets where missing values occur at random.

- **MICE with LightGBM (`'mice+lightgbm'`)**: 
  A variant of MICE that uses LightGBM as the underlying estimator. This method combines the benefits of MICE with the powerful LightGBM algorithm.

- **MICE with XGBoost (`'mice+xgboost'`)**: 
  Another variant of MICE, using XGBoost as the estimator. This method is useful for datasets with complex, nonlinear relationships among features.

To specify the imputation method, set the `G` parameter in the `iArt.test` function to one of the above options. For example, to use Bayesian Ridge for imputation:

.. code-block:: python

    result = iArt.test(Z=Z, X=X, Y=Y, G='bayesianridge', L=1000, verbose=True)

Choose the imputation method that best fits the characteristics of your data and the requirements of your analysis.

Custom Imputation Method
------------------------

You have the option to create a personalized imputation approach by utilizing the `IterativeImputer` class with an estimator parameter.
This flexibility allows for a bespoke approach to your specific data and imputation requirements, such as enabling GPU support or parallel computing, ensuring a tailored fit to your unique needs.

Example of creating a custom imputation strategy:

.. code-block:: python

    from sklearn.experimental import enable_iterative_imputer
    from sklearn.impute import IterativeImputer
    import lightgbm as lgb

    # Configure LightGBM parameters for GPU usage
    lgb_params = {
        'device': 'gpu',  # This enables GPU
        # Add other LightGBM parameters as needed
    }

    # Create a LightGBM model with GPU support
    lgb_model = lgb.LGBMRegressor(**lgb_params)

    # Use this model in IterativeImputer
    custom_imputer = IterativeImputer(estimator=lgb_model)

    # Set the G parameter in iArt to the custom imputer
    G = custom_imputer

For guidance on constructing your own imputation method in scikit-learn, visit the `IterativeImputer` documentation: `IterativeImputer <https://scikit-learn.org/stable/modules/generated/sklearn.impute.IterativeImputer.html>`_.

Additionally, refer to this resource for understanding the standards for scikit-learn estimators: `Developing scikit-learn estimators <https://scikit-learn.org/stable/developers/develop.html>`_.

Handling Strata in the Data
---------------------------

Stratification in data analysis is a technique used to ensure that different subpopulations are adequately represented. In the iArt package, you can incorporate strata into your analysis using the `S` parameter in the `iArt.test` function. 

The `S` parameter requires an array indicating the stratum index for each data point. Each unique value in this array represents a different stratum. The function then considers these strata during the analysis, which can be crucial for representative results, especially in heterogeneous populations.

.. code-block:: python

    # S array indicates the stratum index for each data point
    S = np.array([0, 0, 1, 1, 1, 2, 2, 2])
    
    # Incorporating strata into the analysis
    result = iArt.test(Z=Z, X=X, Y=Y, S=S, L=1000, verbose=True)

In this example, the dataset is divided into three strata. The first two data points belong to stratum 0, the next three to stratum 1, and the final three to stratum 2. The `iArt.test` function will perform the analysis by considering these strata, thus accommodating the potential differences and similarities within each stratum.


Covariate Adjustment 
-------------------------------------------

Covariate adjustment in randomization tests is a technique used to control for the effects of observed covariates that might increase the power. In the iArt package, this uses bayesian ridge regression. The `iArt.test` function allows for covariate adjustment.

To enable covariate adjustment in your analysis, set the `covariate_adjustment` parameter to `True` in the `iArt.test` function. This triggers the application of methods detailed in the article, where covariate adjustment algorithm details are described

.. code-block:: python

    # Conducting a randomization test with covariate adjustment
    result = iArt.test(Z=Z, X=X, Y=Y, covariate_adjustment=True, L=1000, verbose=True)

In this example, the `covariate_adjustment=True` argument instructs the `iArt.test` function to adjust for covariates while handling missing data and conducting the randomization test. This approach is particularly beneficial in studies where covariates are believed to influence the treatment effect or when the goal is to improve the robustness of the causal inference.

For more details on the specific algorithms and methods used for covariate adjustment in iArt, refer to the `algorithms.rst` documentation.

Specifying an Alternative Hypothesis:
-------------------------------------

To specify alternative hypothesis, set the `alternative` parameter in the `iArt.test` function to one of the following options:

.. code-block:: python

    # For a one-sided test greater than
    result = iArt.test(Z=Z, X=X, Y=Y, alternative="greater", L=1000, verbose=True)

    # For a one-sided test less than
    result = iArt.test(Z=Z, X=X, Y=Y, alternative="less", L=1000, verbose=True)

    # For a two-sided test
    result = iArt.test(Z=Z, X=X, Y=Y, alternative="two-sided", L=1000, verbose=True)

Setting a Random State for Reproducibility:
-------------------------------------------

To set a random state for reproducibility:

.. code-block:: python

    result = iArt.test(Z=Z, X=X, Y=Y, random_state=42, L=1000, verbose=True)

The `iArt.test` function is versatile and can be adapted to various scenarios in causal studies, especially those with missing data. The examples above demonstrate different ways to use the function to suit specific research needs.

API
-------------------------------------------
The iArt package provides the `iArt.test` function for conducting finite-population-exact randomization tests in causal studies, particularly when dealing with missing outcomes. This function is a cornerstone of the iArt package, enabling the application of design-based causal inference in various research scenarios.

.. autosummary::
   :toctree: generated

   iArt.test
