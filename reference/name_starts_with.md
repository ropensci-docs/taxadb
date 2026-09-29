# scientific name starts with

scientific name starts with

## Usage

``` r
name_starts_with(
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
name_starts_with("Trochalop")
#> # A tibble: 100 × 15
#>    taxonID  scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>    <chr>    <chr>          <chr>     <chr>               <chr>           <chr>  
#>  1 ITIS:12… Trochaloptero… species   ITIS:1282088        synonym         Animal…
#>  2 ITIS:12… Trochalopteru… subspeci… ITIS:919100         synonym         Animal…
#>  3 ITIS:12… Trochaloptero… subspeci… ITIS:919063         synonym         Animal…
#>  4 ITIS:12… Trochaloptero… subspeci… ITIS:919060         synonym         Animal…
#>  5 ITIS:12… Trochaloptero… subspeci… ITIS:919066         synonym         Animal…
#>  6 ITIS:91… Trochaloptero… subspeci… ITIS:1282602        synonym         Animal…
#>  7 ITIS:91… Trochaloptero… subspeci… ITIS:919033         accepted        Animal…
#>  8 ITIS:91… Trochaloptero… subspeci… ITIS:919034         accepted        Animal…
#>  9 ITIS:91… Trochaloptero… subspeci… ITIS:919050         accepted        Animal…
#> 10 ITIS:91… Trochaloptero… subspeci… ITIS:919054         accepted        Animal…
#> # ℹ 90 more rows
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>
# }
```
