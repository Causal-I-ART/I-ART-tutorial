Contributing to I-ART
=====================

We welcome contributions to the I-ART project! Whether you're interested in fixing bugs, adding new features, or improving documentation, your help is appreciated. This document provides guidelines and instructions for contributing to I-ART.

Getting Started
---------------

Before you begin contributing to I-ART, you should have:

- A GitHub account
- A basic understanding of version control with Git
- Familiarity with Python programming

Setting Up Your Development Environment
---------------------------------------

1. **Fork the Repository**: Start by forking the I-ART repository on GitHub.

2. **Clone Your Fork**: Clone your forked repository to your local machine.

   .. code-block:: console

      git clone https://github.com/Causal-I-ART/I-ART.git
      cd i_art

3. **Create a Virtual Environment** (Optional but recommended):

   .. code-block:: console

      python -m venv venv
      source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

4. **Install Development Dependencies**:

   .. code-block:: console

      pip install -r requirements.txt

Making Changes
--------------

1. **Create a New Branch**:

   .. code-block:: console

      git checkout -b your-new-feature

2. **Make Your Changes**: Add your changes to the codebase, making sure to adhere to the existing coding style.

3. **Test Your Changes**: Run existing tests and add new ones if necessary.

Submitting Your Contribution
----------------------------

1. **Commit Your Changes**:

   .. code-block:: console

      git add .
      git commit -m "Add a brief description of your changes"

2. **Push to Your Fork**:

   .. code-block:: console

      git push origin your-new-feature

3. **Create a Pull Request**: Go to the original I-ART repository on GitHub and create a pull request from your forked repository.

Contributor Code of Conduct
---------------------------

The I-ART project adheres to a code of conduct that all contributors are expected to follow. This ensures a welcoming and inclusive environment for everyone.

Reporting Issues
----------------

If you find bugs or have suggestions for improvements, please create an issue on the GitHub repository. Be sure to include as much information as possible, such as:

- The version of I-ART you're using
- Steps to reproduce the issue
- Expected and actual outcomes

Thank you for considering contributing to I-ART!
