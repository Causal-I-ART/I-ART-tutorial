Welcome to iArt's documentation!
=================================

**iArt** (Imputation-Assisted Randomization Tests) is finite-population-exact randomization tests in design-based causal studies with
missing outcomes.

Design-based causal inference, also known as randomization-based or finite-population causal inference, is one of the most widely used causal inference frameworks, largely due to the merit that its statistical validity can be guaranteed by the study design (e.g., randomized experiments) and does not require assuming specific outcome-generating distributions or super-population models. Despite its advantages, design-based causal inference can still suffer from other data-related issues, among which outcome missingness is a prevalent and significant challenge. This work systematically studies the outcome missingness problem in design-based causal inference. First, we propose a general and flexible outcome missingness mechanism that can facilitate finite-population-exact randomization tests for the null effect. Second, under this flexible missingness mechanism, we propose a general framework called ``imputation and re-imputation" for conducting finite-population-exact randomization tests in design-based causal inference with missing outcomes. This framework can incorporate any imputation algorithms (from linear models to advanced machine learning-based imputation algorithms) while ensuring finite-population-exact type-I error rate control. Third, we extend our framework to conduct covariate adjustment in randomization tests and construct finite-population-valid confidence sets with missing outcomes. Our framework is evaluated via extensive simulation studies and applied to a large-scale randomized experiment. Corresponding Python and R packages are also developed.


.. note::

   iArt is an open-source project, available in Python and R packages. We actively encourage contributions, bug reports, and feature suggestions!

Article
-----------------
For more detailed theoretical background and methodologies implemented in the iArt package, you can refer to the following article:

`Design-Based Causal Inference with Missing Outcomes: Missingness Mechanisms, Imputation-Assisted Randomization Tests, and Covariate Adjustment <https://arxiv.org/abs/2310.18556>`_

.. raw:: html

    <iframe src="https://arxiv.org/pdf/2310.18556.pdf" width="700" height="388" style="border: none;">Your browser does not support PDFs. Download the PDF to view it: <a href="https://arxiv.org/pdf/2310.18556.pdf">Download PDF</a>.</iframe>

GitHub
-----------------
The source code for all iArt is available on GitHub:

`iArt on GitHub <https://github.com/orgs/Imputation-Assisted-Randomization-Tests/repositories>`_

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
