# 04b. Logistic regression

## The data

For this lab we load the Small-cell Lung Cancer dataset (see
[codebook](https://cuny-epibios.github.io/PUBH614/articles/dataset_sclc.md)).

When working with files in R, it’s important to know what your working
directory is, and where the file that you want to load is. This lab uses
webR/WASM, which runs in your web browser and is isolated from your
computer’s filesystem. You’ll see that this R session is in an empty
directory that exists only in this session and not otherwise on your
computer.

Please enable JavaScript to experience the dynamic code cell content on
this page.

Please enable JavaScript to experience the dynamic code cell content on
this page.

You would use these same commands when running R on your computer, but
you would see the same directories and files as in your file explorer.

Since the webR/WASM filesystem is isolated from your local filesystem,
we’ll use
[`download.file()`](https://rdrr.io/r/utils/download.file.html) to
download the dataset from the web, instead of clicking in a web browser.
You could use Dropbox etc to create a downloadable URL for another file
you want to use.

Datasets for PUBH614 labs are kept at
<https://github.com/CUNY-epibios/PUBH614/tree/main/datasets>. After
clicking on a dataset, be sure to press the “Raw” button to get the URL
for the raw dataset, as opposed to the HTML page displaying it. For this
dataset, it is
<https://raw.githubusercontent.com/CUNY-epibios/PUBH614/refs/heads/main/datasets/Stats4-%20more.csv>.

The `destfile` argument specifies what filename to use for the
downloaded file.

Please enable JavaScript to experience the dynamic code cell content on
this page.

Check now that this file has been downloaded:

Please enable JavaScript to experience the dynamic code cell content on
this page.

`readr` provides `read_csv`, a more powerful version of the base-R
`read.csv` function.

Please enable JavaScript to experience the dynamic code cell content on
this page.

If you are using RStudio, the “File - Import Dataset” option provides a
much simplified way to find datasets on your local filesystem and import
them - see
[here](https://support.posit.co/hc/en-us/articles/218611977-Importing-Data-with-the-RStudio-IDE).

## Smoking and Lung Cancer Analysis

There are other functions such as read_xlsx for other types of excel
sheets.

Use glimpse to see what’s there:

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Cross-tabulation of Smoking and Lung Cancer

Compare with slide 8 of session 4:

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Logistic Regression Analysis

#### Basic Model: Smoking and Lung Cancer

Please enable JavaScript to experience the dynamic code cell content on
this page.

The coefficients are in log odds, so we exponentiate to get the odds
ratio for smoking on lung cancer:

Please enable JavaScript to experience the dynamic code cell content on
this page.

#### Adjusted Model: Smoking, Lung Cancer, and Sex

Please enable JavaScript to experience the dynamic code cell content on
this page.

Note that this is now adjusted for sex.

#### Sex-specific Estimates

##### Analysis for Men

Please enable JavaScript to experience the dynamic code cell content on
this page.

##### Analysis for Women

Please enable JavaScript to experience the dynamic code cell content on
this page.

This demonstrates that estimating odds ratios from a suitable two-by-two
table gives you the same answer as using logistic regression, but
logistic regression is much easier to use, particularly when adjusting
for confounders. However, you do need to have your data in the right
format - here, a row for each person with their smoking status, lung
cancer status, and sex.

## Job Callback Analysis

### Initial Data Exploration

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Gender Analysis

#### Callback by Gender

Please enable JavaScript to experience the dynamic code cell content on
this page.

#### Logistic Regression for Gender

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Education Analysis

#### Callback by Years of College

Please enable JavaScript to experience the dynamic code cell content on
this page.

#### Logistic Regression for Education

Please enable JavaScript to experience the dynamic code cell content on
this page.

#### Adjusted Education Analysis

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Race Analysis

#### Callback by Race

Please enable JavaScript to experience the dynamic code cell content on
this page.

#### Basic Race Model

Please enable JavaScript to experience the dynamic code cell content on
this page.

#### Adjusted Race Model

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Experience Analysis

#### Overall Experience Effect

Please enable JavaScript to experience the dynamic code cell content on
this page.

#### Experience Effect by Demographics

##### For Black Candidates

Please enable JavaScript to experience the dynamic code cell content on
this page.

##### For White Candidates

Please enable JavaScript to experience the dynamic code cell content on
this page.

##### For Male Candidates

Please enable JavaScript to experience the dynamic code cell content on
this page.

##### For Female Candidates

Please enable JavaScript to experience the dynamic code cell content on
this page.

------------------------------------------------------------------------

[![Creative Commons
License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)  
This work is licensed under a [Creative Commons Attribution-ShareAlike
4.0 International
License](http://creativecommons.org/licenses/by-sa/4.0/).
