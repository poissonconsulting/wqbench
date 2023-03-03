
# wqbench

<!-- badges: start -->
<!-- badges: end -->

The goal of wqbench is to …

## Installation

``` r
# install.packages("devtools")
devtools::install_github("poissonconsulting/wqbench")
```

## Workflow

This is a basic example which shows you how to solve a common problem:

``` r
library(wqbench)
```

### Compile Data Set

Download the most recent database

``` r
download_path <- wqb_download_epa_ecotox("data_download")
```

Create a SQLite database from the Downloaded Ecotox Data

``` r
database_09_22 <- wqb_create_epa_ecotox(
  file_path = "ecotox_db",
  data_path = "data_dl/ecotox_ascii_09_15_2022"
)
```

Add and update database

- all these functions need to be run for the data set to compile.

``` r
bc_species <- wqb_add_bc_species(
  database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
) 

chem_bc_wqg <- wqb_add_bc_wqg(
  database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
)

conc_endpoints <- wqb_add_concentration_endpoints(
  database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
)

lifestage_codes <- wqb_add_lifestage(
  database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
) 

media_groups <- wqb_add_media(
 database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
)

trophic_groups <- wqb_add_trophic_group(
  database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
) 

duration_unit_code_standardization <- wqb_standardize_duration(
  database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
)

concentration_unit_code_standardization <- wqb_standardize_concentration(
  database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
)

data_compiled <- wqb_compile_dataset(
  database = "ecotox_db/ecotox_ascii_09_15_2022.sqlite"
) 
data_compiled
```

### Classify Duration

Once the data set has been compiled, the duration can be set.
