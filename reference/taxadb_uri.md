# Locate the Parquet files backing a taxadb table

Locate the Parquet files backing a taxadb table

## Usage

``` r
taxadb_uri(
  provider = getOption("taxadb_default_provider", "itis"),
  schema = c("dwc", "common"),
  version = latest_version(),
  local = NULL
)
```

## Arguments

- provider:

  from which provider should the hierarchy be returned? Default is
  'itis', which can also be configured using
  `options(default_taxadb_provider=...")`. See `[td_create]` for a list
  of recognized providers.

- schema:

  One of "dwc" (for Darwin Core data) or "common" (for the Common names
  table.)

- version:

  Which version of the taxadb provider database should we use? defaults
  to latest. See
  [`available_versions()`](https://docs.ropensci.org/taxadb/reference/available_versions.md)
  for details.

- local:

  should we return the path to a local snapshot? By default a local copy
  is used when one is present (see
  [`td_download()`](https://docs.ropensci.org/taxadb/reference/td_download.md)),
  and the remote snapshot is streamed otherwise.

## Value

a glob pattern (or file path) that `duckdb` can read

## Examples

``` r
taxadb_uri("itis_test")
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/taxadb/extdata/dwc_itis_test.parquet"
```
