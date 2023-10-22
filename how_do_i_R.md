make package:

library(usethis)

usethis::create_package("path")

usethis::use_package("pkg") # to add package to description

use_roxygen_md()

https://usethis.r-lib.org/


make documentation:

library(devtools)

devtools::document()

devtools::load_all()

http://r-pkgs.had.co.nz/


do testing:

usethis::test_that() # init test folder

usethis::use_test("name") # autogenerates test file

devtools::test() # run tests


Sweave:
R CMD Sweave chapter1.Rnw
    ## will produce chapter1.tex

format:
<<opts>>==
R code
@

opts= fig, echo
e.g. fig=TRUE etc.
