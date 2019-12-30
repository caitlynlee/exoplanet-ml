# Exoplanet ML

Machine learning models and utilities for exoplanet science.

## Original code

This repo forked from https://github.com/google-research/exoplanet-ml

## Walkthrough

You can jump straight to the [AstroNet walkthrough](exoplanet-ml/astronet/README.md#walkthrough).

# Setup

## Required Packages

* **TensorFlow** ([instructions](https://www.tensorflow.org/install/))
* **Pandas** ([instructions](http://pandas.pydata.org/pandas-docs/stable/install.html))
* **NumPy** ([instructions](https://docs.scipy.org/doc/numpy/user/install.html))
* **SciPy** ([instructions](https://scipy.org/install.html))
* **AstroPy** ([instructions](http://www.astropy.org/))
* **PyDl** ([instructions](https://pypi.python.org/pypi/pydl))
* **Bazel** ([instructions](https://docs.bazel.build/versions/master/install.html))
* **Abseil Python Common Libraries** ([instructions](https://github.com/abseil/abseil-py))

## Detailed Environemt Setup  

Find a detailed step by step environment setup for getting all the packages built and the unit tests passing [here](EnvironmentSetup.md). 

## Run Unit Tests

Verify that all dependencies are satisfied by running the unit tests:

```bash
cd exoplanet-ml  # Bazel must run from a directory with a WORKSPACE file
bazel test astronet/... astrowavenet/... light_curve/... tf_util/... third_party/...
```
