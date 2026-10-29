# Look up taxonomic information by common name

Look up taxonomic information by common name

## Usage

``` r
filter_common(
  name,
  provider = getOption("taxadb_default_provider", "itis"),
  version = latest_version(),
  collect = TRUE,
  ignore_case = TRUE,
  db = td_connect()
)
```

## Arguments

- name:

  a character vector of common (vernacular English) names, e.g. "Humans"

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

## See also

Other filter_by:
[`filter_by()`](https://docs.ropensci.org/taxadb/reference/filter_by.md),
[`filter_id()`](https://docs.ropensci.org/taxadb/reference/filter_id.md),
[`filter_name()`](https://docs.ropensci.org/taxadb/reference/filter_name.md),
[`filter_rank()`](https://docs.ropensci.org/taxadb/reference/filter_rank.md)

## Examples

``` r
# \donttest{

filter_common("Pied Tamarin")
#> # A tibble: 1 × 15
#>   taxonID   vernacularName language acceptedNameUsageID scientificName taxonRank
#>   <chr>     <chr>          <chr>    <chr>               <chr>          <chr>    
#> 1 ITIS:572… Pied Tamarin   english  ITIS:572923         Saguinus bico… species  
#> # ℹ 9 more variables: taxonomicStatus <chr>, kingdom <chr>, phylum <chr>,
#> #   class <chr>, order <chr>, family <chr>, genus <chr>, specificEpithet <chr>,
#> #   infraspecificEpithet <chr>

# }
```
