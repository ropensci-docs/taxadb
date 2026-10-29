# Providers taxadb can rebuild

Providers taxadb can rebuild

## Usage

``` r
taxadb_providers()
```

## Value

a character vector of provider abbreviations

## Details

Unlike
[`available_providers()`](https://docs.ropensci.org/taxadb/reference/available_providers.md),
which reports what is published, this reports what
[`td_build()`](https://docs.ropensci.org/taxadb/reference/td_build.md)
knows how to derive from the provider's own distribution.

## Examples

``` r
taxadb_providers()
#> [1] "itis" "ncbi" "col"  "gbif" "ott"  "fb"   "slb" 
```
