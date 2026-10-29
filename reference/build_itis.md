# Rebuild the ITIS snapshot

Rebuild the ITIS snapshot

## Usage

``` r
build_itis(
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

  path to the ITIS SQLite archive; downloaded if missing

- dir:

  directory for build inputs and outputs

- db:

  a duckdb connection

## Value

the paths written, invisibly

## Details

ITIS distributes a SQLite database, which duckdb reads directly.
`n_usage` carries the accepted/synonym distinction under two
vocabularies, zoological (`valid`/`invalid`) and botanical
(`accepted`/`not accepted`); both map onto `accepted` and `synonym`.

ITIS assigns a TSN to synonyms as well as accepted names, so every row
here carries its own `taxonID` – which makes ITIS the reference for the
taxadb rules checked by
[`td_validate()`](https://docs.ropensci.org/taxadb/reference/td_validate.md).

`scientificNameAuthorship` is taken from ITIS's own author table, keyed
on the author id together with the kingdom, since the id is only unique
within one.

## See also

Other build:
[`build_col()`](https://docs.ropensci.org/taxadb/reference/build_col.md),
[`build_fishbase()`](https://docs.ropensci.org/taxadb/reference/build_fishbase.md),
[`build_gbif()`](https://docs.ropensci.org/taxadb/reference/build_gbif.md),
[`build_ncbi()`](https://docs.ropensci.org/taxadb/reference/build_ncbi.md),
[`build_ott()`](https://docs.ropensci.org/taxadb/reference/build_ott.md)

## Examples

``` r
if (FALSE) { # \dontrun{
build_itis("2026")
} # }
```
