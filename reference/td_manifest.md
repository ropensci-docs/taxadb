# Describe a built snapshot

Describe a built snapshot

## Usage

``` r
td_manifest(
  version = format(Sys.Date(), "%Y"),
  dir = build_dir(),
  validate = TRUE,
  db = td_connect()
)
```

## Arguments

- version:

  the snapshot version to describe

- dir:

  the build output directory, see
  [`build_dir()`](https://docs.ropensci.org/taxadb/reference/build_dir.md)

- validate:

  should each table be checked with
  [`td_validate()`](https://docs.ropensci.org/taxadb/reference/td_validate.md)
  and the result recorded? Default `TRUE`. Archival snapshots predate
  the schema rules and will report violations; recording them is the
  point.

- db:

  a duckdb connection

## Value

a data.frame with one row per published table, giving its provider,
schema, row count, columns, file sizes and checksum, and the upstream
release it was derived from.

## Details

Run after
[`td_build()`](https://docs.ropensci.org/taxadb/reference/td_build.md).
The row counts and checksums are read back off the written files rather
than carried over from the build, so the manifest describes what was
actually published.

## Examples

``` r
if (FALSE) { # \dontrun{
td_manifest("2026")
} # }
```
