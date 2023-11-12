Welcome to iArt's documentation!
=================================

**iArt** (Imputation-Assisted Randomization Tests) is finite-population-exact randomization tests in design-based causal studies with
missing outcomes.

Design-based (also known as finite-population or randomization-based) causal inference is one of the most widely used frameworks for testing causal null hypotheses or
inferring about causal parameters from experimental or observational data. The most
significant merit of design-based causal inference is that its statistical validity only
comes from the study design (e.g., randomization design in a randomized experiment)
and does not require assuming any outcome-generating distributions or models. Although immune to model misspecification, design-based causal inference can still suffer
from other data challenges, among which missingness in outcomes is a significant one.
However, compared with model-based (also known as super-population or samplingbased) causal inference, outcome missingness in design-based causal inference is much
less studied, largely due to the challenge that design-based causal inference does not
assume any outcome distributions/models and, therefore, cannot directly adopt any
existing model-based approaches for missing data. To fill this gap, we systematically study the missing outcomes problem in design-based causal inference. First, we
use the potential outcomes framework to clarify the minimal assumption (concerning
the outcome missingness mechanism) needed for conducting finite-population-exact
randomization tests for the null effect (i.e., Fisher’s sharp null) and that needed for
constructing finite-population-exact confidence sets with missing outcomes. Second,
we propose a general framework called “imputation and re-imputation" for conducting finite-population-exact randomization tests in design-based causal studies with
missing outcomes. Our framework can incorporate any existing outcome imputation
algorithms and meanwhile guarantee finite-population-exact type-I error rate control.
Third, we extend our framework to conduct covariate adjustment in an exact randomization test with missing outcomes and to construct finite-population-exact confidence
sets with missing outcomes. We conduct comprehensive simulation studies to examine
exact type-I error rate control and gains in power using our framework. We have also
developed an open-source Python and R package for implementation of our methods.

.. note::

   iArt is an open-source project, available in Python and R packages. We actively encourage contributions, bug reports, and feature suggestions!

Article
-----------------
For more detailed theoretical background and methodologies implemented in the iArt package, you can refer to the following article:

`Design-Based Causal Inference with Missing Outcomes: Missingness Mechanisms, Imputation-Assisted Randomization Tests, and Covariate Adjustment <https://arxiv.org/abs/2310.18556>`_

.. raw:: html

    <iframe src="_static/2310.18556.pdf" width="700" height="388" style="border: none;">Your browser does not support PDFs. Download the PDF to view it: <a href="_static/2310.18556.pdf">Download PDF</a>.</iframe>


GitHub
-----------------
The source code for all iArt is available on GitHub:

`iArt on GitHub <https://github.com/Imputation-Assisted-Randomization-Tests/python-iArt>`_

Python
-----------------
You can also find iArt on PyPI:

`iArt on PyPI <https://pypi.org/project/python-iArt/>`_

R
-----------------
You can also find iArt here:

`iArt on R <https://github.com/Imputation-Assisted-Randomization-Tests/iArt/>`_


Citation
-----------------
If you use iArt in your research, please consider citing:

.. code-block:: bibtex

   @misc{heng2023designbased,
         title={Design-Based Causal Inference with Missing Outcomes: Missingness Mechanisms, Imputation-Assisted Randomization Tests, and Covariate Adjustment},
         author={Siyu Heng and Jiawei Zhang and Yang Feng},
         year={2023},
         eprint={2310.18556},
         archivePrefix={arXiv},
         primaryClass={stat.ME}
   }

Contents
-----------------

.. toctree::
   :maxdepth: 2

   python-package
   R-package
   difference
   contributing
   license
   references
