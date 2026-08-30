# Match names that start or contain a specified text string

Match names that start or contain a specified text string

## Usage

``` r
fuzzy_filter(
  name,
  by = c("scientificName", "vernacularName"),
  provider = getOption("taxadb_default_provider", "itis"),
  match = c("contains", "starts_with"),
  version = latest_version(),
  db = td_connect(),
  ignore_case = TRUE,
  collect = TRUE
)
```

## Arguments

- name:

  vector of names (scientific or common, see `by`) to be matched
  against.

- by:

  a column name in the taxa_tbl (following Darwin Core Schema terms).
  The filtering join is executed with this column as the joining
  variable.

- provider:

  from which provider should the hierarchy be returned? Default is
  'itis', which can also be configured using
  `options(default_taxadb_provider=...")`. See `[td_create]` for a list
  of recognized providers.

- match:

  should we match by names starting with the term or containing the term
  anywhere in the name?

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

- collect:

  logical, default `TRUE`. Should we return an in-memory data.frame
  (default, usually the most convenient), or a reference to lazy-eval
  table on disk (useful for very large tables on which we may first
  perform subsequent filtering operations.)

## Details

Note that fuzzy filter will be fast with an single or small number of
names, but will be slower if given a very large vector of names to
match, as unlike other `filter_` commands, fuzzy matching requires
separate SQL calls for each name. As fuzzy matches should all be
confirmed manually in any event, e.g. not every common name containing
"monkey" belongs to a primate species.

This method utilizes the database operation `%like%` to filter tables
without loading into memory. Note that this does not support the use of
regular expressions at this time.

## Examples

``` r
# \donttest{

## match any common name containing:
name <- c("woodpecker", "monkey")
fuzzy_filter(name, "vernacularName")
#> # A tibble: 19 × 15
#>    taxonID  scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>    <chr>    <chr>          <chr>     <chr>               <chr>           <chr>  
#>  1 ITIS:99… Saimiri colli… species   ITIS:998637         accepted        Animal…
#>  2 ITIS:94… Saimiri cassi… subspeci… ITIS:945136         accepted        Animal…
#>  3 ITIS:57… Saimiri boliv… species   ITIS:572979         accepted        Animal…
#>  4 ITIS:57… Saimiri oerst… species   ITIS:572980         accepted        Animal…
#>  5 ITIS:18… Cebidae        family    ITIS:180093         accepted        Animal…
#>  6 ITIS:94… Saimiri cassi… species   ITIS:944148         accepted        Animal…
#>  7 ITIS:94… Saimiri boliv… subspeci… ITIS:945139         accepted        Animal…
#>  8 ITIS:94… Saimiri sciur… subspeci… ITIS:180095         synonym         Animal…
#>  9 ITIS:94… Saimiri sciur… subspeci… ITIS:998637         synonym         Animal…
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

## match scientific name
fuzzy_filter("Trochalop", "scientificName",
             match = "starts_with")
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
