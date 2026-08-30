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
#>  1 ITIS:91… Trochaloptero… species   ITIS:1282059        synonym         Animal…
#>  2 ITIS:12… Trochaloptero… species   ITIS:1282061        synonym         Animal…
#>  3 ITIS:12… Trochaloptero… species   ITIS:919057         synonym         Animal…
#>  4 ITIS:12… Trochaloptero… subspeci… ITIS:919063         synonym         Animal…
#>  5 ITIS:12… Trochaloptero… subspeci… ITIS:916125         synonym         Animal…
#>  6 ITIS:12… Trochaloptero… subspeci… ITIS:919067         synonym         Animal…
#>  7 ITIS:12… Trochaloptero… subspeci… ITIS:1282602        accepted        Animal…
#>  8 ITIS:91… Trochaloptero… subspeci… ITIS:1282060        synonym         Animal…
#>  9 ITIS:91… Trochaloptero… subspeci… ITIS:1282061        synonym         Animal…
#> 10 ITIS:91… Trochaloptero… subspeci… ITIS:916116         synonym         Animal…
#> # ℹ 90 more rows
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>
# }
```
