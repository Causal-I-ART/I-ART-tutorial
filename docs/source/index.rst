Welcome to I-ART's documentation!
=================================

**I-ART** (Imputation-Assisted Randomization Tests) is a Python package designed for conducting finite-population-exact randomization tests in design-based causal studies with missing outcomes. It leverages the potential outcomes framework and integrates various outcome imputation algorithms to offer a robust solution for handling missing data in causal inference.

This package is particularly useful for researchers and practitioners in the fields of statistics, epidemiology, social sciences, and any other domain where causal inference from experimental or observational data is crucial.

For more detailed information on how to install and use I-ART, including its diverse functionalities and practical examples, refer to the :doc:`usage` section.

.. note::

   I-ART is an open-source project and is actively maintained. Contributions, bug reports, and feature suggestions are welcome!

Article
-----------------
For more detailed theoretical background and methodologies implemented in the I-ART package, you can refer to the following article:

`Design-Based Causal Inference with Missing Outcomes: Missingness Mechanisms, Imputation-Assisted Randomization Tests, and Covariate Adjustment <https://arxiv.org/abs/2310.18556>`_

.. raw:: html

    <iframe src="_static/2310.18556.pdf" width="700" height="388" style="border: none;">Your browser does not support PDFs. Download the PDF to view it: <a href="_static/2310.18556.pdf">Download PDF</a>.</iframe>


GitHub
-----------------
The source code for I-ART is available on GitHub:

`I-ART on GitHub <https://github.com/Imputation-Assisted-Randomization-Tests/py-I-ART>`_

PyPI
-----------------
You can also find I-ART on PyPI:

`I-ART on PyPI <https://pypi.org/project/py-i-art/>`_

Citation
-----------------
If you use I-ART in your research, please consider citing:

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
   api
   contributing
   license
