# Labs for CUNY SPH PUBH 614 <img src="man/figures/CUNYlogo.png" align="right" width="75" height="75" alt="logo"/>

# Quick-start

Note the menu bars:
- **OpenIntro Labs**: Labs from [OpenIntro Statistics][OpenIntro]
- **Other Labs**: Labs from other sources
- **Datasets**: Codebooks for datasets used in labs
- **Exercises**: Practice exercises (currently only contains a blank workbook that
you can use to run R in your browser)

Datasets for these labs are stored in a GitHub repository [here](https://github.com/CUNY-epibios/PUBH614/tree/main/datasets).

# About WASM and webR

These labs use **[WASM]** (WebAssembly) and **[webR]** to provide a user-friendly 
alternative for running R directly in your browser. This approach eliminates the 
need for local installation or a Cloud service, and allows for interactive 
coding and visualizationwithin the browser environment.

Running R in your web browser can sometimes lead to issues such as:

- **Performance Limitations**: Browser-based execution may be slower compared to 
local execution. Even if you have a powerful computer, your browser likely only
supports up to 4GB of memory for WebAssembly applications.
- **Browser Compatibility**: Ensure you are using a modern browser that supports 
WebAssembly, such as a current version of Chrome, Firefox, Safari, or Edge.
- **Data Storage**: Data is stored in your browser's local storage, which is 
separated from your local filesystem. This means that data and code are not 
persistent across sessions, and you will lose your work if you close the browser.
You can print the page to save your work, or copy the code to a local text file.


[webR]: https://docs.r-wasm.org/webr/latest/
[WASM]: https://developer.mozilla.org/en-US/docs/WebAssembly

# About OpenIntro Labs

These labs were developed by [OpenIntro Statistics][OpenIntro] and adapted for 
use on the web by Levi Waldron at CUNY SPH. OpenIntro Labs promote the 
understanding and application of statistics through applied data analysis. 
Labs are titled based on topic area, which correspond to particular chapters in 
all three versions of OpenIntro Statistics, a free and open-source textbook. 
The textbook as well as original versions of the labs can be found at 
[https://www.openintro.org/book/ims/](https://www.openintro.org/book/ims/). 
Use the **Labs** button above to see all available labs.

[OpenIntro]: https://www.openintro.org/

# About R and how to use these labs

## What are R and CRAN?

**R** is a powerful programming language and environment specifically designed 
for statistical computing and graphics. It is widely used among statisticians 
and data scientists for data analysis and visualization. **CRAN** (Comprehensive 
R Archive Network) is a repository that hosts R packages, which are collections 
of R functions, data, and compiled code that extend the capabilities of R. 
CRAN hosts more than 20,000 active packages, or libraries, each adding extra
functionality to R [[1](https://cran.r-project.org)].

### How is R Different from SAS and SPSS?

R is an open-source language, which means it is free to use and has a large 
community contributing to its development. Unlike **SAS** and **SPSS**, which 
are commercial software with licensing fees, R offers flexibility and a vast 
array of packages for various statistical techniques. R is highly 
customizable and preferred in academic and research environments for its 
extensibility and active community support.

## RStudio: A Powerful IDE for R

[RStudio] is a popular integrated development environment (IDE) for running R. 
It provides a user-friendly interface, tools for plotting, history, debugging, 
and workspace management. While RStudio is powerful, it does have a learning 
curve, especially for those new to programming or R. You can install R and 
RStudio for free on your own computer [here][RStudio].

[RStudio]: https://posit.co/download/rstudio-desktop/

## Cloud Services for Running R

There are several cloud services that offer free tiers for running R, making it 
accessible without the need for local installation:

- [posit.cloud] is cloud-based service by Posit (formerly RStudio) 
that allows you to run R and RStudio using your browser. The
free tier has limited resources but is sufficient for running the labs in this
course. Note: whereas https://cuny-epibios.github.io/PUBH614/ runs code in your 
browser and it is actually running on your computer, [posit.cloud] and other
cloud services run code on a remote server.
- [Google Colab](https://colab.research.google.com/) is another cloud-based 
service that uses Jupyter notebooks, an alternative system for running code 
interactively. Jupyter notebooks are widely used in data science and machine 
learning, and are less feature-rich and simpler to use than RStudio. Google 
Colab provides more generous resources in the free tier cheaper paid tiers than
posit.cloud, and makes use of your Google Drive for storage.

[posit.cloud]: https://posit.cloud/

## Reporting Issues

If you encounter any issues, notice any errors or problems, or have suggestions
for improvement, please let Levi Waldron and other potential contributors know 
by [opening an issue](https://github.com/CUNY-epibios/PUBH614/issues).

## Building this site

Test individual labs from the command-line:
```sh
quarto render vignettes/01_intro_to_r.qmd
```

Rebuild entire site from R:
```R
pkgdown::build_site()
```

Modify website layout in `_pkgdown.yml`, modify custom css in `pkgdown/custom.css`.

<a rel="license" href="https://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="https://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

