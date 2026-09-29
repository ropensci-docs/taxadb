# Rebuild the NCBI Taxonomy snapshot

Rebuild the NCBI Taxonomy snapshot

## Usage

``` r
build_ncbi(
  version = format(Sys.Date(), "%Y"),
  archive = NULL,
  dir = build_dir(),
  db = td_connect()
)
```

## Arguments

- version:

  snapshot version to write, e.g. `"2026"`

- archive:

  path to the NCBI `taxdump.tar.gz`; downloaded if missing

- dir:

  directory for build inputs and outputs

- db:

  a duckdb connection

## Value

the paths written, invisibly

## Details

NCBI distributes `nodes.dmp` (the hierarchy) and `names.dmp` (every
name), in a format that claims to be tab-separated but delimits fields
with `\\t|\\t`.

Every row of `names.dmp` carries the `tax_id` of the *accepted* taxon,
whatever the name's class: NCBI mints no separate identifier for a
synonym. So the `scientific name` rows become the accepted names,
carrying a `taxonID` and pointing `acceptedNameUsageID` at themselves,
and every other name class becomes a row for the same taxon with a
`NULL` `taxonID` – which the taxadb rules permit, since there is no
identifier to give.

## See also

Other build:
[`build_col()`](https://docs.ropensci.org/taxadb/reference/build_col.md),
[`build_fishbase()`](https://docs.ropensci.org/taxadb/reference/build_fishbase.md),
[`build_gbif()`](https://docs.ropensci.org/taxadb/reference/build_gbif.md),
[`build_itis()`](https://docs.ropensci.org/taxadb/reference/build_itis.md),
[`build_ott()`](https://docs.ropensci.org/taxadb/reference/build_ott.md)

## Examples

``` r
if (FALSE) { # \dontrun{
build_ncbi("2026")
} # }
```
