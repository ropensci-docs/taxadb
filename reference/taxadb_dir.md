# Show the local taxadb directory

Show the local taxadb directory

## Usage

``` r
taxadb_dir()
```

## Value

path to the local taxadb data directory

## Details

Local snapshots downloaded by
[`td_download()`](https://docs.ropensci.org/taxadb/reference/td_download.md)
are stored here. Override with the `TAXADB_HOME` environment variable.

## Examples

``` r
taxadb_dir()
#> [1] "/tmp/RtmpZNCq87/taxadb"
```
