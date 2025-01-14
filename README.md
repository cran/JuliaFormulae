
<!-- README.md is generated from README.Rmd. Please edit that file -->

# JuliaFormulae

<!-- badges: start -->

[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://lifecycle.r-lib.org/articles/stages.html#experimental)
[![R-CMD-check](https://github.com/yjunechoe/JuliaFormulae/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/yjunechoe/JuliaFormulae/actions/workflows/R-CMD-check.yaml)
[![Codecov test
coverage](https://codecov.io/gh/yjunechoe/JuliaFormulae/branch/main/graph/badge.svg)](https://app.codecov.io/gh/yjunechoe/JuliaFormulae?branch=main)
<!-- badges: end -->

A utility package for converting R regression model formula to Julia
[GLM.jl](https://github.com/JuliaStats/GLM.jl) and
[MixedModels.jl](https://github.com/JuliaStats/MixedModels.jl) syntax.

See [`{jlme}`](https://github.com/yjunechoe/jlme) for an example
application.

## Installation

``` r
# install.packages("devtools")
devtools::install_github("yjunechoe/JuliaFormulae")
```

``` r
library(JuliaFormulae)
```

## Supported conversions

- Zero correlation:

  ``` r
  julia_formula(y ~ x + (x || g))
  #> y ~ x + zerocorr(x | g)
  ```

- Protection:

  ``` r
  julia_formula(y ~ x + I(x * 2))
  #> y ~ x + protect(x * 2)
  ```

- Interaction terms:

  ``` r
  julia_formula(y ~ a:b)
  #> y ~ a & b
  ```

## Example

``` r
julia_formula(
  y ~ a + I(a * 2) + b + a:b  + (a || g) + (b | g)
)
#> y ~ a + protect(a * 2) + b + (a & b) + zerocorr(a | g) + (b | 
#>     g)
```
