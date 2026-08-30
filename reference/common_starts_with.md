# common name starts with

common name starts with

## Usage

``` r
common_starts_with(
  name,
  provider = getOption("taxadb_default_provider", "itis"),
  version = latest_version(),
  db = td_connect(),
  ignore_case = TRUE
)
```

## Arguments

- name:

  vector of names (scientific or common, see `by`) to be matched
  against.

- provider:

  from which provider should the hierarchy be returned? Default is
  'itis', which can also be configured using
  `options(default_taxadb_provider=...")`. See `[td_create]` for a list
  of recognized providers.

- version:

  Which version of the taxadb provider database should we use? defaults
  to latest. See
  [`available_versions()`](https://docs.ropensci.org/taxadb/reference/available_versions.md)
  for details.

- db:

  a connection to the taxadb database. See details.

- ignore_case:

  should we ignore case (capitalization) in matching names? Can be
  significantly slower to run.

## Examples

``` r
# \donttest{
common_starts_with("monkey")
#> # A tibble: 0 × 15
#> # ℹ 15 variables: taxonID <chr>, scientificName <chr>, taxonRank <chr>,
#> #   acceptedNameUsageID <chr>, taxonomicStatus <chr>, kingdom <chr>,
#> #   phylum <chr>, class <chr>, order <chr>, family <chr>, genus <chr>,
#> #   specificEpithet <chr>, infraspecificEpithet <chr>, vernacularName <chr>,
#> #   update_date <chr>
# }
```
