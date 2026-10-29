# Write the metadata published with a snapshot

Writes `manifest.csv` and `README.md` into the snapshot directory, ready
to be uploaded alongside the Parquet files.

## Usage

``` r
td_write_metadata(
  version = format(Sys.Date(), "%Y"),
  dir = build_dir(),
  repo = taxadb_repo(),
  archival = FALSE,
  db = td_connect()
)
```

## Arguments

- version:

  the snapshot version to describe

- dir:

  the build output directory, see
  [`build_dir()`](https://docs.ropensci.org/taxadb/reference/build_dir.md)

- repo:

  the data repository the snapshot will be published to

- archival:

  is this a republication of a historical release rather than a fresh
  build? Archival snapshots are byte-identical to what that version
  originally contained, so they predate the current schema rules and the
  README says so.

- db:

  a duckdb connection

## Value

the paths written, invisibly

## Details

The README states what the tables are, what the schema means, where each
provider's data came from and under what licence, so that someone who
finds the data without the package can still use it.

## Examples

``` r
if (FALSE) { # \dontrun{
td_write_metadata("2026")
} # }
```
