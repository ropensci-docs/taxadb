# Check a taxadb table against the taxadb Darwin Core rules

Check a taxadb table against the taxadb Darwin Core rules

## Usage

``` r
td_validate(
  provider = getOption("taxadb_default_provider", "itis"),
  schema = c("dwc", "common"),
  version = latest_version(),
  db = td_connect()
)
```

## Arguments

- provider:

  from which provider should the hierarchy be returned? Default is
  'itis', which can also be configured using
  `options(default_taxadb_provider=...")`. See `[td_create]` for a list
  of recognized providers.

- schema:

  One of "dwc" (for Darwin Core data) or "common" (for the Common names
  table.)

- version:

  Which version of the taxadb provider database should we use? defaults
  to latest. See
  [`available_versions()`](https://docs.ropensci.org/taxadb/reference/available_versions.md)
  for details.

- db:

  a connection to the taxadb database. See details.

## Value

a data.frame with one row per rule, giving whether the table `pass`es,
how many rows `violations` were found, and a `note`.

## Details

The rules checked are:

- **columns** – the required Darwin Core terms are present, spelled in
  Darwin Core camelCase.

- **types** – identifier and name columns are character. A column that
  is entirely `NA` will often be typed as integer or logical by mistake,
  which this catches.

- **scientificName** – never `NA`. Every row names something, at every
  rank: `Animalia` is a scientificName just as `Homo sapiens` is.

- **taxonRank**, **taxonomicStatus** – never `NA`.

- **acceptedNameUsageID** – never `NA`, on synonyms *and* on accepted
  names. This is where taxadb is stricter than Darwin Core.

- **accepted_has_id** – a row labelled `accepted` is its own accepted
  name: `taxonID` is present and equals `acceptedNameUsageID`.
  (`taxonID` may be `NA` on a synonym, where the provider mints no
  identifier for it – OTT and NCBI, for instance, do not.)

- **accepted_resolves** – every `acceptedNameUsageID` matches the
  `taxonID` of a self-referencing row. No dangling references.

- **synonym_not_self** – a row labelled a synonym points somewhere else,
  never at itself.

- **taxonID_one_name** – a `taxonID` always names the same
  `scientificName`. An identifier may appear on more than one row: ITIS
  records 255 synonyms that are ambiguous between two accepted taxa, and
  a row for each is the honest representation. What must not happen is
  one identifier naming two *different* names, which is what results
  from a provider numbering its accepted names and its synonyms in
  separate sequences and both being given the same prefix.

- **accepted_unique** – no duplicate `taxonID` among accepted names.

- **id_prefix** – identifiers are the provider's identifier prefixed by
  the provider abbreviation in capitals, e.g. `ITIS:180092`.

`taxonomicStatus` is deliberately *not* checked against a controlled
vocabulary: providers draw real distinctions (`homotypic synonym`,
`provisionally accepted`, `doubtful`, `misapplied`) that are worth
preserving. The rules are therefore phrased structurally. A name the
provider does not redirect to another name is its own accepted name
whatever confidence it expresses about it, so `doubtful` and
`provisionally accepted` rows self-reference exactly as `accepted` ones
do; only the two terms whose meaning taxadb actually relies on,
`accepted` and `synonym`, are given a required shape.

## Examples

``` r
# \donttest{
td_validate("itis_test")
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpZNCq87/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>     provider schema version                rule pass violations
#> 1  itis_test    dwc    <NA>             columns TRUE          0
#> 2  itis_test    dwc    <NA>               types TRUE          0
#> 3  itis_test    dwc    <NA>      scientificName TRUE          0
#> 4  itis_test    dwc    <NA>           taxonRank TRUE          0
#> 5  itis_test    dwc    <NA>     taxonomicStatus TRUE          0
#> 6  itis_test    dwc    <NA> acceptedNameUsageID TRUE          0
#> 7  itis_test    dwc    <NA>     accepted_has_id TRUE          0
#> 8  itis_test    dwc    <NA>    synonym_not_self TRUE          0
#> 9  itis_test    dwc    <NA>           id_prefix TRUE          0
#> 10 itis_test    dwc    <NA>   accepted_resolves TRUE          0
#> 11 itis_test    dwc    <NA>    taxonID_one_name TRUE          0
#> 12 itis_test    dwc    <NA>     accepted_unique TRUE          0
#>                                                      note
#> 1                                       dwc terms present
#> 2                 identifier and name columns are VARCHAR
#> 3                               scientificName never NULL
#> 4                                    taxonRank never NULL
#> 5                              taxonomicStatus never NULL
#> 6                          acceptedNameUsageID never NULL
#> 7              accepted names are their own accepted name
#> 8                          synonyms point to another name
#> 9                            identifiers prefixed 'ITIS:'
#> 10 every acceptedNameUsageID resolves to an accepted name
#> 11                  each taxonID names one scientificName
#> 12                           one row per accepted taxonID
# }
```
