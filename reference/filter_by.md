# Creates a data frame with column name given by `by`, and values given by the vector `x`, and then uses this table to do a filtering join, joining on the `by` column to return all rows matching the `x` values (scientificNames, taxonIDs, etc).

Creates a data frame with column name given by `by`, and values given by
the vector `x`, and then uses this table to do a filtering join, joining
on the `by` column to return all rows matching the `x` values
(scientificNames, taxonIDs, etc).

## Usage

``` r
filter_by(
  x,
  by,
  provider = getOption("taxadb_default_provider", "itis"),
  schema = c("dwc", "common"),
  version = latest_version(),
  collect = TRUE,
  db = td_connect(),
  ignore_case = FALSE
)
```

## Arguments

- x:

  a vector of values to filter on

- by:

  a column name in the taxa_tbl (following Darwin Core Schema terms).
  The filtering join is executed with this column as the joining
  variable.

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

- collect:

  logical, default `TRUE`. Should we return an in-memory data.frame
  (default, usually the most convenient), or a reference to lazy-eval
  table on disk (useful for very large tables on which we may first
  perform subsequent filtering operations.)

- db:

  a connection to the taxadb database. See details.

- ignore_case:

  should we ignore case (capitalization) in matching names? Can be
  significantly slower to run.

## Value

a data.frame in the Darwin Core tabular format containing the matching
taxonomic entities.

## See also

Other filter_by:
[`filter_common()`](https://docs.ropensci.org/taxadb/reference/filter_common.md),
[`filter_id()`](https://docs.ropensci.org/taxadb/reference/filter_id.md),
[`filter_name()`](https://docs.ropensci.org/taxadb/reference/filter_name.md),
[`filter_rank()`](https://docs.ropensci.org/taxadb/reference/filter_rank.md)

## Examples

``` r
# \donttest{

sp <- c("Trochalopteron henrici gucenense",
        "Trochalopteron elliotii")
filter_by(sp, "scientificName")
#> # A tibble: 2 × 15
#>   taxonID   scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>   <chr>     <chr>          <chr>     <chr>               <chr>           <chr>  
#> 1 ITIS:924… Trochaloptero… subspeci… ITIS:916116         synonym         Animal…
#> 2 ITIS:916… Trochaloptero… species   ITIS:916116         accepted        Animal…
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>

filter_by(c("ITIS:180092", "ITIS:916116"), "taxonID")
#> # A tibble: 2 × 15
#>   taxonID   scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>   <chr>     <chr>          <chr>     <chr>               <chr>           <chr>  
#> 1 ITIS:180… Homo sapiens   species   ITIS:180092         accepted        Animal…
#> 2 ITIS:916… Trochaloptero… species   ITIS:916116         accepted        Animal…
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>

filter_by("Aves", "class")
#> # A tibble: 1,803 × 15
#>    taxonID  scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>    <chr>    <chr>          <chr>     <chr>               <chr>           <chr>  
#>  1 ITIS:91… Trochaloptero… species   ITIS:1282059        synonym         Animal…
#>  2 ITIS:92… Aphelocoma ca… subspeci… ITIS:924065         accepted        Animal…
#>  3 ITIS:72… Cyanocorax sa… species   ITIS:559631         synonym         Animal…
#>  4 ITIS:72… Pica hudsonia  species   ITIS:726117         accepted        Animal…
#>  5 ITIS:72… Cyanocorax sa… subspeci… ITIS:726126         accepted        Animal…
#>  6 ITIS:72… Cyanocorax sa… subspeci… ITIS:726127         accepted        Animal…
#>  7 ITIS:12… Corvus caryoc… species   ITIS:561630         synonym         Animal…
#>  8 ITIS:12… Nucifraga mac… species   ITIS:924176         synonym         Animal…
#>  9 ITIS:12… Nucifraga ows… species   ITIS:1276448        synonym         Animal…
#> 10 ITIS:12… Corvus columb… species   ITIS:179750         synonym         Animal…
#> # ℹ 1,793 more rows
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>

# }
```
