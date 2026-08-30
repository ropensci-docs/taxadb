# return all taxa in which scientific name contains the text provided

return all taxa in which scientific name contains the text provided

## Usage

``` r
name_contains(
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
name_contains("Trochalop")
#> # A tibble: 100 × 15
#>    taxonID  scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>    <chr>    <chr>          <chr>     <chr>               <chr>           <chr>  
#>  1 ITIS:12… Trochalopterum genus     ITIS:915740         synonym         Animal…
#>  2 ITIS:12… Trochaloptero… species   ITIS:1282085        synonym         Animal…
#>  3 ITIS:12… Trochaloptero… species   ITIS:1282667        synonym         Animal…
#>  4 ITIS:12… Trochaloptero… species   ITIS:919071         synonym         Animal…
#>  5 ITIS:12… Trochaloptero… species   ITIS:919053         synonym         Animal…
#>  6 ITIS:12… Trochaloptero… subspeci… ITIS:919024         synonym         Animal…
#>  7 ITIS:12… Trochaloptero… subspeci… ITIS:919062         synonym         Animal…
#>  8 ITIS:12… Trochaloptero… subspeci… ITIS:919063         synonym         Animal…
#>  9 ITIS:12… Trochaloptero… subspeci… ITIS:919064         synonym         Animal…
#> 10 ITIS:12… Trochaloptero… subspeci… ITIS:919065         synonym         Animal…
#> # ℹ 90 more rows
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>
# }
```
