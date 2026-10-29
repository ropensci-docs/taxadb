# Rebuild the Catalogue of Life snapshot

Rebuild the Catalogue of Life snapshot

## Usage

``` r
build_col(
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

  path to the COL Darwin Core Archive; downloaded if missing

- dir:

  directory for build inputs and outputs

- db:

  a duckdb connection

## Value

the paths written, invisibly

## Details

COL publishes a Darwin Core Archive whose `scientificName` carries the
authorship – `Acanthocerataceae Crawford & Round`. taxadb wants the
canonical name, since authorship abbreviations vary too much between
providers to match on. COL also supplies `scientificNameAuthorship`
separately, so the canonical name is the one with that suffix removed.

COL marks accepted names by leaving `acceptedNameUsageID` empty, and
distinguishes `accepted` from `provisionally accepted`; both are
accepted in the sense that matters here, that they are not a synonym of
anything else, so both get `acceptedNameUsageID` set to their own
`taxonID`.

## See also

Other build:
[`build_fishbase()`](https://docs.ropensci.org/taxadb/reference/build_fishbase.md),
[`build_gbif()`](https://docs.ropensci.org/taxadb/reference/build_gbif.md),
[`build_itis()`](https://docs.ropensci.org/taxadb/reference/build_itis.md),
[`build_ncbi()`](https://docs.ropensci.org/taxadb/reference/build_ncbi.md),
[`build_ott()`](https://docs.ropensci.org/taxadb/reference/build_ott.md)

## Examples

``` r
if (FALSE) { # \dontrun{
build_col("2026")
} # }
```
