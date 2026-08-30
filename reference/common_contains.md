# common name starts with

common name starts with

## Usage

``` r
common_contains(
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
common_contains("monkey")
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpZNCq87/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> # A tibble: 19 × 15
#>    taxonID  scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>    <chr>    <chr>          <chr>     <chr>               <chr>           <chr>  
#>  1 ITIS:57… Saimiri boliv… species   ITIS:572979         accepted        Animal…
#>  2 ITIS:57… Saimiri oerst… species   ITIS:572980         accepted        Animal…
#>  3 ITIS:18… Cebidae        family    ITIS:180093         accepted        Animal…
#>  4 ITIS:94… Saimiri cassi… species   ITIS:944148         accepted        Animal…
#>  5 ITIS:94… Saimiri boliv… subspeci… ITIS:945139         accepted        Animal…
#>  6 ITIS:94… Saimiri sciur… subspeci… ITIS:180095         synonym         Animal…
#>  7 ITIS:94… Saimiri sciur… subspeci… ITIS:998637         synonym         Animal…
#>  8 ITIS:99… Saimiri colli… species   ITIS:998637         accepted        Animal…
#>  9 ITIS:94… Saimiri cassi… subspeci… ITIS:945136         accepted        Animal…
#> 10 ITIS:57… Saimiri ustus  species   ITIS:572981         accepted        Animal…
#> 11 ITIS:57… Saimiri vanzo… species   ITIS:572982         accepted        Animal…
#> 12 ITIS:18… Saimiri sciur… species   ITIS:180095         accepted        Animal…
#> 13 ITIS:94… Saimiri macro… species   ITIS:944149         accepted        Animal…
#> 14 ITIS:94… Saimiri oerst… subspeci… ITIS:945134         accepted        Animal…
#> 15 ITIS:94… Saimiri cassi… subspeci… ITIS:945135         accepted        Animal…
#> 16 ITIS:55… Cebinae        subfamily ITIS:552350         accepted        Animal…
#> 17 ITIS:18… Saimiri        genus     ITIS:180094         accepted        Animal…
#> 18 ITIS:94… Saimiri oerst… subspeci… ITIS:945133         accepted        Animal…
#> 19 ITIS:94… Saimiri boliv… subspeci… ITIS:945140         accepted        Animal…
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>
# }
```
