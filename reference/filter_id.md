# Return a taxonomic table matching the requested ids

Return a taxonomic table matching the requested ids

## Usage

``` r
filter_id(
  id,
  provider = getOption("taxadb_default_provider", "itis"),
  type = c("taxonID", "acceptedNameUsageID"),
  version = latest_version(),
  collect = TRUE,
  db = td_connect()
)
```

## Arguments

- id:

  taxonomic id, in prefix format

- provider:

  from which provider should the hierarchy be returned? Default is
  'itis', which can also be configured using
  `options(default_taxadb_provider=...")`. See `[td_create]` for a list
  of recognized providers.

- type:

  id type. Can be `taxonID` or `acceptedNameUsageID`, see details.

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

## Value

a data.frame with id and name of all matching species

## Details

Use `type="acceptedNameUsageID"` to return all rows for which this ID is
the accepted ID, including both synonyms and and accepted names (since
both all synonyms of a name share the same `acceptedNameUsageID`.) Use
`taxonID` (default) to only return those rows for which the Scientific
name corresponds to the `taxonID.`

Some providers (e.g. ITIS) assign taxonIDs to synonyms, most others only
assign IDs to accepted names. In the latter case, this means requesting
`taxonID` will only match accepted names, while requesting matches to
the `acceptedNameUsageID` will also return any known synonyms. See
examples.

## See also

Other filter_by:
[`filter_by()`](https://docs.ropensci.org/taxadb/reference/filter_by.md),
[`filter_common()`](https://docs.ropensci.org/taxadb/reference/filter_common.md),
[`filter_name()`](https://docs.ropensci.org/taxadb/reference/filter_name.md),
[`filter_rank()`](https://docs.ropensci.org/taxadb/reference/filter_rank.md)

## Examples

``` r
# \donttest{

filter_id(c("ITIS:180092", "ITIS:916116"))
#> # A tibble: 2 × 15
#>   taxonID   scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>   <chr>     <chr>          <chr>     <chr>               <chr>           <chr>  
#> 1 ITIS:180… Homo sapiens   species   ITIS:180092         accepted        Animal…
#> 2 ITIS:916… Trochaloptero… species   ITIS:916116         accepted        Animal…
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>
filter_id("ITIS:916116", type="acceptedNameUsageID")
#> # A tibble: 5 × 15
#>   taxonID   scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>   <chr>     <chr>          <chr>     <chr>               <chr>           <chr>  
#> 1 ITIS:560… Garrulax elli… species   ITIS:916116         synonym         Animal…
#> 2 ITIS:919… Trochaloptero… subspeci… ITIS:916116         synonym         Animal…
#> 3 ITIS:919… Trochaloptero… subspeci… ITIS:916116         synonym         Animal…
#> 4 ITIS:924… Trochaloptero… subspeci… ITIS:916116         synonym         Animal…
#> 5 ITIS:916… Trochaloptero… species   ITIS:916116         accepted        Animal…
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>

# }
```
