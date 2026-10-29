# Rebuild the Open Tree Taxonomy snapshot

Rebuild the Open Tree Taxonomy snapshot

## Usage

``` r
build_ott(
  version = format(Sys.Date(), "%Y"),
  archive = NULL,
  ott_version = "3.7.3",
  dir = build_dir(),
  db = td_connect()
)
```

## Arguments

- version:

  snapshot version to write, e.g. `"2026"`

- archive:

  path to the OTT release archive; downloaded if missing

- ott_version:

  the OTT release to build from, e.g. `"3.7.3"`

- dir:

  directory for build inputs and outputs

- db:

  a duckdb connection

## Value

the paths written, invisibly

## Details

OTT ships `taxonomy.tsv` and `synonyms.tsv`, both delimited with
`\\t|\\t`. `synonyms.tsv` keys each synonym to the `uid` of the name it
is a synonym *of*: OTT mints no identifier for the synonym itself, so
those rows carry a `NULL` `taxonID`, which the taxadb rules allow.

OTT no longer populates the `type` column of `synonyms.tsv` – it is
empty for all 2.2 million rows in release 3.7.3 – so a synonym is
recorded as `synonym` unless a type is given.

OTT publishes no vernacular names, so there is no `common` table for
this provider;
[`filter_common()`](https://docs.ropensci.org/taxadb/reference/filter_common.md)
warns accordingly.

## See also

Other build:
[`build_col()`](https://docs.ropensci.org/taxadb/reference/build_col.md),
[`build_fishbase()`](https://docs.ropensci.org/taxadb/reference/build_fishbase.md),
[`build_gbif()`](https://docs.ropensci.org/taxadb/reference/build_gbif.md),
[`build_itis()`](https://docs.ropensci.org/taxadb/reference/build_itis.md),
[`build_ncbi()`](https://docs.ropensci.org/taxadb/reference/build_ncbi.md)

## Examples

``` r
if (FALSE) { # \dontrun{
build_ott("2026")
} # }
```
