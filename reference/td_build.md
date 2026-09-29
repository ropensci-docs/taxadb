# Rebuild taxadb snapshots from the providers

Runs a provider's preprocessing end to end: fetch the provider's own
distribution, normalize it to the taxadb Darwin Core schema, and write
the Parquet snapshot.

## Usage

``` r
td_build(
  provider = "itis",
  version = format(Sys.Date(), "%Y"),
  dir = build_dir(),
  validate = TRUE,
  db = td_connect(),
  ...
)
```

## Arguments

- provider:

  one or more providers to build. See
  [`taxadb_providers()`](https://docs.ropensci.org/taxadb/reference/taxadb_providers.md).

- version:

  the snapshot version to write, defaults to the year.

- dir:

  directory for build inputs and outputs, see
  [`build_dir()`](https://docs.ropensci.org/taxadb/reference/build_dir.md).

- validate:

  should each table be checked with
  [`td_validate()`](https://docs.ropensci.org/taxadb/reference/td_validate.md)
  after it is written? Default `TRUE`.

- db:

  a duckdb connection

- ...:

  passed to the individual provider builder, e.g. `archive` to use an
  already-downloaded copy.

## Value

a data.frame of the validation results, invisibly if `validate` is
`FALSE` the paths written.

## Details

Snapshots are published for the providers so that most users never need
to run this. It is here so that a user who needs a fresher snapshot than
the published one, or who wants to check how a table was derived, can
rebuild it themselves rather than asking someone to.

Builds are done entirely in `duckdb`, out of core, so they are bounded
by disk rather than memory. The archives are large: COL and GBIF are
around 500MB and 1GB compressed respectively, and are cached in `dir`
between builds.

## Examples

``` r
if (FALSE) { # \dontrun{
## rebuild one provider
td_build("itis")

## rebuild everything that can be built without credentials
td_build(taxadb_providers())
} # }
```
