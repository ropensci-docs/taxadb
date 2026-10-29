# Disconnect from the taxadb database.

Disconnect from the taxadb database.

## Usage

``` r
td_disconnect(db = td_connect())
```

## Arguments

- db:

  database connection

## Value

invisible `TRUE`

## Details

This function manually closes a connection to the `taxadb` database.

## Examples

``` r
# \donttest{
td_disconnect()
# }
```
