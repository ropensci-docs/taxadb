# Create a local taxadb database

Superseded by
[`td_download()`](https://docs.ropensci.org/taxadb/reference/td_download.md).

## Usage

``` r
td_create(
  provider = getOption("taxadb_default_provider", "itis"),
  schema = c("dwc", "common"),
  version = latest_version(),
  overwrite = FALSE,
  lines = NULL,
  dbdir = NULL,
  db = td_connect()
)
```

## Arguments

- provider:

  a character vector of provider(s) to download. See
  [`available_providers()`](https://docs.ropensci.org/taxadb/reference/available_providers.md)
  for the providers published in a given version.

- schema:

  One of "dwc" (for Darwin Core data) or "common" (for the Common names
  table.)

- version:

  Which version of the taxadb provider database should we use? defaults
  to latest. See
  [`available_versions()`](https://docs.ropensci.org/taxadb/reference/available_versions.md)
  for details.

- overwrite:

  passed to
  [`td_download()`](https://docs.ropensci.org/taxadb/reference/td_download.md)

- lines:

  deprecated, ignored.

- dbdir:

  deprecated, ignored.

- db:

  a connection to the taxadb database. See details.

## Value

the local paths of the downloaded files, invisibly.

## Details

`taxadb` no longer needs to import data before querying it: tables are
read directly from Parquet, streamed from remote storage or from a local
copy. `td_create()` is retained as an alias for
[`td_download()`](https://docs.ropensci.org/taxadb/reference/td_download.md),
which installs a local copy.

## Examples

``` r
if (FALSE) { # \dontrun{
td_create("itis")
} # }
```
