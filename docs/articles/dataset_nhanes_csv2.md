# Codebook and example merging for NHANES Datasets

## Codebook: NHANES Dataset

- **Dataset names:** `PBCD_J.xpt` and `INS_J.xpt`
- **Location:** NHANES datasets and codebooks for all years are
  available [here](https://wwwn.cdc.gov/nchs/nhanes/Default.aspx).
  - There is a [single-page list of all download links and
    codebooks](https://wwwn.cdc.gov/nchs/nhanes/search/datapage.aspx).
  - Direct download links from CDC for the 2017-18
    [PBCD_J.xpt](https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2017/DataFiles/PBCD_J.xpt)
    and
    [INS_J.xpt](https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2017/DataFiles/INS_J.xpt)
  - Backup download links from GitHub for the same
    [PBCD_J.xpt](https://github.com/CUNY-epibios/PUBH614/raw/refs/heads/main/datasets/PBCD_J.xpt)
    and
    [INS_J.xpt](https://github.com/CUNY-epibios/PUBH614/raw/refs/heads/main/datasets/INS_J.xpt)
  - Codebooks for
    [PBCD_J](https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2017/DataFiles/PBCD_J.htm)
    and
    [INS_J](https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2017/DataFiles/INS_J.htm)

### Getting the data

Most browsers will prevent code from downloading binary `.xpt` files
(unless you use a [CORS
proxy](https://gist.github.com/jimmywarting/ac1be6ea0297c16c477e17f8fbe51347)),
so in the following we use a `.csv` conversion of these datasets that
can be downloaded in webR. If you are running R not through webR (ie
through RStudio, Jupyter, or another R client), you can do the following
directly with the `.xpt` files.

Option 1: Download csv versions from GitHub backup (xpt binary download
can be restricted by your browser in webR)

Please enable JavaScript to experience the dynamic code cell content on
this page.

Option 2 (this will work in a normal R session but not webR) - Download
xpt files directly from CDC:

    download.file(
      "https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2017/DataFiles/PBCD_J.xpt",
      destfile = "PBCD_J.xpt"
    )
    download.file(
      "https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2017/DataFiles/INS_J.xpt",
      destfile = "INS_J.xpt"
    )

You then need to load and then merge, or join, these datasets into a
single file. If you are working with the original `.xpt` files, load
them using the [haven](https://haven.tidyverse.org/) package which can
import data from SAS, SPSS, and STATA formats. For example,

    library(haven)
    nhanesPb <- read_xpt("PBCD_J.xpt")

However, in webR we’ll use the csv files downloaded above:

Please enable JavaScript to experience the dynamic code cell content on
this page.

Now join the two datasets, matching by the partipant ID column `SEQN`.
This uses `full_join` from the incredible user-friendly and powerful
[join
functions](https://dplyr.tidyverse.org/articles/base.html?q=join#two-table-verbs)
from the [dplyr](https://dplyr.tidyverse.org/) package.

Please enable JavaScript to experience the dynamic code cell content on
this page.

`full_join` means that all partipants in the `SEQN` column will be
maintained, even if a participant exists only in one of the two
datasets. There are other options, for example `inner_join` keeps only
participants present in both datasets, and `left_join` keeps only
partipants present in the first dataset (the first dataset being
whichever you specify as the first argument to the join function). See
the `dplyr` help on [two table
verbs](https://dplyr.tidyverse.org/articles/base.html?q=join#two-table-verbs)
for more information.

Finally, you may want to simplify the dataset using
[`dplyr::select`](https://dplyr.tidyverse.org/reference/select.html) to
select only the columns you intend to use. You don’t need the `dplyr::`
but I like to include it because if you forgot
[`library(dplyr)`](https://dplyr.tidyverse.org) or
[`library(tidyverse)`](https://tidyverse.tidyverse.org) you would
accidentally use `select` from base R, which has different usage and
would give you an error.

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Getting and joining other NHANES datasets

You can join two datasets like above then join a third dataset, and so
on, repeating as many times as you want. Just make sure to use the same
participant ID (SEQN) and the same NHANES cycle. Here’s a shorthand join
of several 2021-23 datasets, downloaded directly from NHANES then
inner_joined to keep only participants with all data available. These
datasets are:

1.  [Demographic Variables and Sample
    Weights](https://wwwn.cdc.gov/nchs/nhanes/search/datapage.aspx?Component=Demographics&Cycle=2021-2023)
2.  [Dietary Supplement Use 30-day - Total Dietary
    Supplements](https://wwwn.cdc.gov/nchs/nhanes/search/datapage.aspx?Component=Dietary&Cycle=2021-2023)
3.  [Body
    Measures](https://wwwn.cdc.gov/nchs/nhanes/search/datapage.aspx?Component=Examination&Cycle=2021-2023)

We take advantage of the ability of data-loading functions to read data
directly from a URL. `haven`, `readr`, and base-R data-loading functions
can do this. The following code downloads and reads the dataset on the
first line, joins it with the dataset on the second line, and then joins
the result with the dataset on the third line.

This is how you would download directly from CDC, if you’re not using
webR:

    library(haven)
    library(dplyr)
    nhanes2 <- read_xpt("https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2021/DataFiles/DEMO_L.xpt") %>%
      inner_join(read_xpt("https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2021/DataFiles/DSQTOT_L.xpt"), by = "SEQN") %>%
      inner_join(read_xpt("https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2021/DataFiles/BPXO_L.xpt"), by = "SEQN")

And here’s a version that works in webR:

``` r
library(readr)
library(dplyr)
```

    Attaching package: 'dplyr'

    The following objects are masked from 'package:stats':

        filter, lag

    The following objects are masked from 'package:base':

        intersect, setdiff, setequal, union

``` r
nhanes2 <- read_csv("https://github.com/CUNY-epibios/PUBH614/raw/refs/heads/main/datasets/DEMO_L.csv") %>%
  inner_join(read_csv("https://github.com/CUNY-epibios/PUBH614/raw/refs/heads/main/datasets/DSQTOT_L.csv"), by = "SEQN") %>%
  inner_join(read_csv("https://github.com/CUNY-epibios/PUBH614/raw/refs/heads/main/datasets/BPXO_L.csv"), by = "SEQN")
```

    Rows: 11933 Columns: 27

    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    dbl (27): SEQN, SDDSRVYR, RIDSTATR, RIAGENDR, RIDAGEYR, RIDAGEMN, RIDRETH1, ...

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    Warning: One or more parsing issues, call `problems()` on your data frame for details,
    e.g.:
      dat <- vroom(...)
      problems(dat)

    Rows: 8860 Columns: 40
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    dbl (39): SEQN, WTDRD1, DSDCOUNT, DSDANCNT, DSD010, DSD010AN, DSQTKCAL, DSQT...
    lgl  (1): DSQTCAFF

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    Rows: 7801 Columns: 12
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr  (1): BPAOARM
    dbl (11): SEQN, BPAOCSZ, BPXOSY1, BPXODI1, BPXOSY2, BPXODI2, BPXOSY3, BPXODI...

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Success! The data files are directly into the `nhanes2` object *without*
saving files locally. Use
[`readr::write_csv`](https://readr.tidyverse.org/reference/write_delim.html)
or something like it if you want to save the data locally. Take a look
at the dataset to see what you have:

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Dataset Overview

The `nhanes` dataset contains three variables from the 2017-18 NHANES
dataset. The dataset includes 8,366 observations with 3 variables.

### Variables

#### SEQN

- **Description**: Sequence number
- **Type**: Numeric
- **Values**: Various sequence numbers, e.g., 93703, 93704, etc.
- **Missing values**: 0

#### LBXBPB

- **Description**: Blood lead level (ug/dL)
- **Type**: Numeric
- **Values**: Various blood lead levels, e.g., 2.98, 0.74, etc.
- **Missing values**: 1,482

#### LBXIN

- **Description**: Insulin level (uU/mL)
- **Type**: Numeric
- **Values**: Various insulin levels, e.g., 9.72, 5.28, etc.
- **Missing values**: 5,541

### Summary Statistics

- `SEQN` omitted for brevity as it contains unique values for each
  observation.

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Data Quality Notes

- The dataset has missing values in the `LBXBPB` and `LBXIN` columns.

### Acknowledgements

This codebook was drafted by Microsoft Copilot and edited by Levi
Waldron.
