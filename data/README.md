# Data source and preparation

This project uses the UCI Maternal Health Risk dataset.

Source: https://archive.ics.uci.edu/dataset/863/maternal+health+risk

DOI: https://doi.org/10.24432/C5DP5D

License: CC BY 4.0

The raw CSV is not included in this repository package. Download the dataset from UCI and save it as:

`data/Maternal Health Risk Data Set.csv`

The notebook checks this relative path when it loads the data.

The CSV used for this project contains 1,014 rows, while the current UCI metadata page reports 1,013 instances. The analysis reports the dimensions of the file that was actually used and records this difference as a source version issue.

Two observations have HeartRate equal to 7 bpm and are excluded from both modeling strategies. For the primary analysis, exact repeated rows are also removed. Because patient identifiers are not available, that decision is treated as a methodological assumption. A second analysis retains the repeated rows and uses grouped validation so that identical predictor profiles never appear in both training and test data.
