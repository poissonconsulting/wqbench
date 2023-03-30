
# wqbench

<!-- badges: start -->

[![img](https://img.shields.io/badge/Lifecycle-Experimental-339999)](https://github.com/bcgov/repomountie/blob/master/doc/lifecycle-badges.md)
[![R-CMD-check](https://github.com/poissonconsulting/wqbench/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/poissonconsulting/wqbench/actions/workflows/R-CMD-check.yaml)
[![Codecov test
coverage](https://codecov.io/gh/poissonconsulting/wqbench/branch/main/graph/badge.svg)](https://app.codecov.io/gh/poissonconsulting/wqbench?branch=main)
<!-- badges: end -->

## Installation

``` r
# install.packages("devtools")
devtools::install_github("bcgov/wqbench")
```

## Workflow

``` r
library(wqbench)
```

### Create Data Set for App

``` r
data_set <- wqb_create_data_set(
  version = 3
)
```

The function will download the US EPA ECOTOX<sup>1</sup> database,
create a local .sqlite database, add other data sources and filter
conditions, clean and process the data, classify the duration and
standardize the effect.

### Generate Benchmark

#### SSD Example

``` r
data <- wqb_filter_chemical(data_set, "13463677")
data <- wqb_benchmark_method(data)

data_agg <- wqb_aggregate(data) 
data_agg <- wqb_af(data_agg)
ctv <- wqb_generate_ctv(data_agg)
```

Plot data set

``` r
wqb_plot(data)
```

Plot the results

``` r
wqb_plot_ssd(data_agg)
```

#### Deterministic Example

``` r
data <- wqb_filter_chemical(data_set, "1000984359")
data <- wqb_benchmark_method(data)

data_agg <- wqb_aggregate(data) 
data_agg <- wqb_af(data_agg)
ctv <- wqb_generate_ctv(data_agg)
```

Plot data set

``` r
wqb_plot(data)
```

Plot the results

``` r
wqb_plot_det(data_agg)
```

#### Benchmark Value

To calculate the benchmark for the chemical, divide the critical
toxicity value (ctv) by each assessment factor.

``` r
benchmark = ctv / (data_agg$af_bc_species * data_agg$af_salmon * data_agg$af_planktonic *data_agg$af_variation)
```

*SSD* method generates a lower and upper confidence interval
*Deterministic* method only generates an estimate

#### Summary Tables

``` r
wqb_summary_trophic_species(data_agg)
wqb_summary_trophic_groups(data_agg)
wqb_summary_af(data_agg)
```

## Getting Help or Reporting an Issue

To report issues, bugs or enhancements, please file an
[issue](https://github.com/bcgov/wqbench/issues). Check out the
[support](https://github.com/bcgov/wqbench/blob/main/.github/SUPPORT.md)
for more info.

## Code of Conduct

Please note that the wqbench project is released with a [Contributor
Code of
Conduct](https://contributor-covenant.org/version/2/1/CODE_OF_CONDUCT.html).
By contributing to this project, you agree to abide by its terms.

## License

The code is released under the Apache License 2.0

> Copyright 2023 Province of British Columbia
>
> Licensed under the Apache License, Version 2.0 (the “License”); you
> may not use this file except in compliance with the License. You may
> obtain a copy of the License at
>
> <https://www.apache.org/licenses/LICENSE-2.0>
>
> Unless required by applicable law or agreed to in writing, software
> distributed under the License is distributed on an “AS IS” BASIS,
> WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
> implied. See the License for the specific language governing
> permissions and limitations under the License.

## Reference

1.  Olker, J. H., Elonen, C. M., Pilli, A., Anderson, A., Kinziger, B.,
    Erickson, S., Skopinski, M., Pomplun, A., LaLone, C. A., Russom, C.
    L., & Hoff, D. (2022). The ECOTOXicology Knowledgebase: A Curated
    Database of Ecologically Relevant Toxicity Tests to Support
    Environmental Research and Risk Assessment. Environmental Toxicology
    and Chemistry, 41(6):1520-1539. <https://doi.org/10.1002/etc.5324>
