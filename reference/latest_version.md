# The most recent taxadb snapshot version

The most recent taxadb snapshot version

## Usage

``` r
latest_version(db = td_connect())
```

## Arguments

- db:

  a connection from
  [`td_connect()`](https://docs.ropensci.org/taxadb/reference/td_connect.md)

## Value

the latest available version, as a character string

## Details

Versions are ordered as version numbers, not as strings. This matters:
as strings `"22.12"` sorts after `"2026"`, so a plain
[`max()`](https://rdrr.io/r/base/Extremes.html) would make an archival
release from 2022 the default for every query once it was published.

## Examples

``` r
if (FALSE) { # \dontrun{
latest_version()
} # }
```
