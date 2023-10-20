# CSCD01 Pandas Overflow

## Set Up Pandas Environment With Our Repo

1. Enter the Pandas folder in our repo `cd pandas-copy`
2. We used Docker to create our environment. To build the Docker image and the run the container: <br>`docker build -t pandas-dev .` <br>`docker run -it --rm -v ${PWD}:/home/pandas pandas-dev` <br>
3. Then run `python setup.py build_ext -j 4` and then <br>`python -m pip install -e . --no-build-isolation --no-use-pep517` to build and install Pandas.

## How To Test for Deliverable 3

### Acceptance Tests

A written format of our user acceptance tests can be viewed in our Deliverable 3 document where we outline sequences of steps for users to follow in order to verify correctness.  
<br>
We have also provided example acceptance tests that are located in **pandas-copy/acceptance_tests**. These are all .py file that can each be run individually `python issue[#].py`. The files are named according to the related issue in our document.

### Run Unit Tests

Run the following commands to run all unit tests created for each issue: <br>

- Issue 1: `pytest pandas/tests/io/formats/style/test_format.py`
  - The `test_format_escape_latex_math()` function contains the unit tests for the issue.
- Issue 2: `pytest pandas/tests/series/methods/test_combine_first.py`
  - The `test_combine_first_preserves_dtype(self)` function contains the unit tests for the issue.
- Issue 3: `pytest pandas/tests/arrays/categorical/test_dtypes.py`
  - The `test_categories_match_up_to_permutation(self)` contains the unit tests for the issue.

## How To Test for Deliverable 4

### Acceptance Tests
A written format of our user acceptance tests can be viewed in our Deliverable 4 document where we outline sequences of steps for users to follow in order to verify correctness.  
<br>
We have also provided example acceptance tests that are located in **pandas-copy/acceptance_tests_D4**. These are all .py file that can each be run individually `python issue[#].py`. The files are named according to the related issue in our document.

### Run Unit Tests

Run the following commands to run all unit tests created for each issue: <br>

- Issue 1: [ENH: Support reduction methods on Index](https://github.com/pandas-dev/pandas/issues/50021)
  - `pytest pandas/tests/indexes/test_reductions.py`
  - `test_kurt()`, `test_skew()`, `test_sem()` and `test_*_fail()` contain unit tests for successful and error cases for those three methods.
  - `test_count()`, `test_sum()`, `test_product()`, and `test_*_fail()` contain unit tests for testing reduction methods: count, sum, and product.
  - `test_mean()`, `test_median()`, `test_std()`, `test_var()`, and `test_*_fail()` contain unit tests for successful and error cases for those methods, respectively.

- Issue 2: [ENH: Allow easy selection of ordered/unordered categorical columns](https://github.com/pandas-dev/pandas/issues/46941)
  - Solution 1: `pytest pandas/tests/frame/methods/test_select_dtypes.py`
  - The `test_select_dtypes_ordered()` function contains the unit tests for the issue with solution 1 implementation.
  - Solution 2: `pytest pandas/tests/frame/accessors/test_cat_accessor.py`
    - The `TestCatAccessorDataframe` class contains all unit tests for the issue with solution 2 implementation.
