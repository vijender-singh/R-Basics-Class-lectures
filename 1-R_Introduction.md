## R Introduction

#### Origin

`R` originated from `S`.   `S` was a statistical programming language developed by John Chambers in 1976 at Bell labs. `S` was a properitory software and was not available for researchers.  **R**obert Gentleman and **R**oss Ihaka, University of Auckland, New Zealand came up with the idea of `R` as an free open source statistical language in 1992.  In 1995 they released its initial version and a stable beta version was released in 2000. Since `R` is implemented from `S` combined with lexical scoping semantics, inspired by Scheme. 

The latest release (2018-12-20, Eggshell Igloo) R-3.5.2 .
The Comprehensive R archive Network (CRAN : https://cran.r-project.org/) is a network of ftp and web servers around the world that store identical, upup-to-date, versions of code and documentation for R.

### Packages:

The primary reason for the popularity and success of R is its collection of user-contributed packages.
At present CRAN hosts 13,711 packages and 1560 by bioconductor contributed by user community. A package is a library of prewritten code to accomplish a given set of tasks. e.g. `ggplot2` is a package with functions for plotting and `dplyr` is for manipulating data objects.

### Installing Packages

#### CRAN Packages
The packages in CRAN are open to anyone to submit their package.
Using R studio tabs `Tools > Install Packages` and provide the name of package and also tick install dependencies. Change the installation directory if separate installation directory is required.

##### or 

through CLI 
```{R}
install.packages("ggplot2")
```
to install from git hub try
```{R}
install_github(repo="coefplot")
```
###Bioconductor packages
Bio conductor provides tools for the analysis and comprehension of high-throughput genomic data. Bio conductor uses the R statistical programming language, and is open source and open development.

Source `biocLite.R` to install bi conductor packages in older version of R (3.4 and older)

```{R}
source("http://bioconductor.org/biocLite.R")
```
to install a package
```{R}
biocLite("edgeR",version="3.8")
```

`BiocManager` is for managing Bio conductor packages in R>3.5.  To load BiocManager,
```{R}
if (!requireNamespace("BiocManager"))
    install.packages("BiocManager")
BiocManager::install()
```
to install a package
```{R}
BiocManager::install("edgeR", version = "3.8")
```

Once the packages are installed they are required to be loaded to use the functions/code inside the package. Both `require` and `library` function help in loading the packages.
```{R}
require(EdgeR)
```
or 
```{R}
library(EdgeR)
```
To suppress the messages that are displayed on loading a package set `quietly=TRUE`
```{R}
require(EdgeR, quietly=TRUE)
```
**Unloading a package**
```{R}
detach("EdgeR")
```

**Important:**

It is quite possible for functions in different packages to have the same name. For example `coefplot` is in both `arm` and `coefplot`.  If both packages are loaded, the `coefplot` function will be executed from the package that was loaded last (or more recent). A way around this is to precede the function with the name of the package, separated by two colons (::).
```{R}
arm::coefplot(object)
coefplot::coefplot(object)
