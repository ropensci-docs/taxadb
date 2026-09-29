# The taxadb data repository

The taxadb data repository

## Usage

``` r
taxadb_repo()
```

## Value

the object-store prefix holding taxadb snapshots.

## Details

Override with `options(taxadb_repo=)` or the `TAXADB_REPO` environment
variable to read from a mirror or a staging repository.

## Examples

``` r
taxadb_repo()
#> [1] "cboettig/taxadb"
```
