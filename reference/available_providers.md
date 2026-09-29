# Name providers available for a given version

Name providers available for a given version

## Usage

``` r
available_providers(version = latest_version(), db = td_connect())
```

## Arguments

- version:

  snapshot version, defaults to the latest available

- db:

  a connection from
  [`td_connect()`](https://docs.ropensci.org/taxadb/reference/td_connect.md)

## Value

a data.frame of `provider` and the `schema`s published for it

## Examples

``` r
if (FALSE) { # \dontrun{
available_providers()
} # }
```
