# Install a local copy of a taxadb snapshot

Downloads the Parquet files for the requested provider(s) into
[`taxadb_dir()`](https://docs.ropensci.org/taxadb/reference/taxadb_dir.md),
so that subsequent queries read from local disk instead of streaming
from remote storage.

## Usage

``` r
td_download(
  provider = getOption("taxadb_default_provider", "itis"),
  schema = c("dwc", "common"),
  version = latest_version(),
  overwrite = FALSE,
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

  should we re-download files that are already present? Default `FALSE`.

- db:

  a connection to the taxadb database. See details.

## Value

the local paths of the downloaded files, invisibly.

## Details

Streaming is fast enough for most interactive use and requires no setup,
so a local copy is optional. Install one when you will make many queries
against the same table, when you need to work offline, or when you want
a snapshot pinned on disk for reproducibility.

Snapshots are large: the Darwin Core tables for `col` and `gbif` are
each several hundred MB. Use
[`available_providers()`](https://docs.ropensci.org/taxadb/reference/available_providers.md)
to see what is published, and delete a local copy with
`unlink(taxadb_dir(), recursive = TRUE)`.

## Examples

``` r
if (FALSE) { # \dontrun{
## Install a local copy of ITIS. Writes to taxadb_dir() and downloads
#  tens of MB, so this is never run unattended.
td_download("itis")
} # }
```
