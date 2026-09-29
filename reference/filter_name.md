# Look up taxonomic information by scientific name

Look up taxonomic information by scientific name

## Usage

``` r
filter_name(
  name,
  provider = getOption("taxadb_default_provider", "itis"),
  version = latest_version(),
  collect = TRUE,
  ignore_case = FALSE,
  db = td_connect()
)
```

## Arguments

- name:

  a character vector of scientific names, e.g. "Homo sapiens"

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

- collect:

  logical, default `TRUE`. Should we return an in-memory data.frame
  (default, usually the most convenient), or a reference to lazy-eval
  table on disk (useful for very large tables on which we may first
  perform subsequent filtering operations.)

- ignore_case:

  should we ignore case (capitalization) in matching names? Can be
  significantly slower to run.

- db:

  a connection to the taxadb database. See details.

## Value

a data.frame in the Darwin Core tabular format containing the matching
taxonomic entities.

## Details

Most but not all authorities can match against both species level and
higher-level (or lower, e.g. subspecies or variety) taxonomic names. The
rank level is indicated by `taxonRank` column.

Most authorities include both known synonyms and accepted names in the
`scientificName` column, (with the status indicated by
`taxonomicStatus`). This is convenient, as users will typically not know
if the names they have are synonyms or accepted names, but will want to
get the match to the accepted name and accepted ID in either case.

## See also

Other filter_by:
[`filter_by()`](https://docs.ropensci.org/taxadb/reference/filter_by.md),
[`filter_common()`](https://docs.ropensci.org/taxadb/reference/filter_common.md),
[`filter_id()`](https://docs.ropensci.org/taxadb/reference/filter_id.md),
[`filter_rank()`](https://docs.ropensci.org/taxadb/reference/filter_rank.md)

## Examples

``` r
# \donttest{

sp <- c("Trochalopteron henrici gucenense",
        "Trochalopteron elliotii")
filter_name(sp)
#> # A tibble: 2 × 15
#>   taxonID   scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>   <chr>     <chr>          <chr>     <chr>               <chr>           <chr>  
#> 1 ITIS:924… Trochaloptero… subspeci… ITIS:916116         synonym         Animal…
#> 2 ITIS:916… Trochaloptero… species   ITIS:916116         accepted        Animal…
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>

# }
```
