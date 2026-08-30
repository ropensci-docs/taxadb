# List the taxonomic snapshots available from the taxadb repository

List the taxonomic snapshots available from the taxadb repository

## Usage

``` r
list_snapshots(db = td_connect())
```

## Arguments

- db:

  a connection from
  [`td_connect()`](https://docs.ropensci.org/taxadb/reference/td_connect.md)

## Value

a data.frame with one row per published Parquet file, giving its
`version`, `schema`, `provider` and `uri`.

## Details

Requires network access. Results are cached for the session.

## Examples

``` r
if (FALSE) { # \dontrun{
list_snapshots()
} # }
```
