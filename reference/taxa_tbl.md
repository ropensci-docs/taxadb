# Return a reference to a given table in the taxadb database

Return a reference to a given table in the taxadb database

## Usage

``` r
taxa_tbl(
  provider = getOption("taxadb_default_provider", "itis"),
  schema = c("dwc", "common"),
  version = latest_version(),
  db = td_connect()
)
```

## Arguments

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

- db:

  a connection to the taxadb database. See details.

## Value

a lazy `dplyr` table backed by the requested Parquet snapshot.

## Details

The returned table is a `duckdb` view over Parquet, so it can be
manipulated with any `dplyr` verb and is only ever read to the extent
your query requires. Unless a local copy has been installed with
[`td_download()`](https://docs.ropensci.org/taxadb/reference/td_download.md),
the data is streamed from remote storage on demand.

## Examples

``` r
# \donttest{

  ## default schema is the Darwin Core table
  taxa_tbl()
#> # A query:  ?? x 15
#> # Database: DuckDB 1.5.5 [unknown@Linux 6.17.0-1022-azure:R 4.6.0/:memory:]
#>    taxonID  scientificName taxonRank acceptedNameUsageID taxonomicStatus kingdom
#>    <chr>    <chr>          <chr>     <chr>               <chr>           <chr>  
#>  1 ITIS:10… Leontopithecu… species   ITIS:1025093        synonym         Animal…
#>  2 ITIS:10… Midas tripart… species   ITIS:1025098        synonym         Animal…
#>  3 ITIS:10… Hapale nigrif… species   ITIS:1025100        synonym         Animal…
#>  4 ITIS:10… Midas bicolor  species   ITIS:572923         synonym         Animal…
#>  5 ITIS:10… Leontocebus m… subspeci… ITIS:1207742        synonym         Animal…
#>  6 ITIS:10… Saguinus fusc… subspeci… ITIS:1025157        synonym         Animal…
#>  7 ITIS:10… Leontocebus w… species   ITIS:1025102        accepted        Animal…
#>  8 ITIS:10… Leontocebus w… subspeci… ITIS:1025155        accepted        Animal…
#>  9 ITIS:10… Leontocebus w… subspeci… ITIS:1025156        accepted        Animal…
#> 10 ITIS:10… Leontocebus w… subspeci… ITIS:1025157        accepted        Animal…
#> # ℹ more rows
#> # ℹ 9 more variables: phylum <chr>, class <chr>, order <chr>, family <chr>,
#> #   genus <chr>, specificEpithet <chr>, infraspecificEpithet <chr>,
#> #   vernacularName <chr>, update_date <chr>

  ## common names table
  taxa_tbl(schema = "common")
#> # A query:  ?? x 15
#> # Database: DuckDB 1.5.5 [unknown@Linux 6.17.0-1022-azure:R 4.6.0/:memory:]
#>    taxonID  vernacularName language acceptedNameUsageID scientificName taxonRank
#>    <chr>    <chr>          <chr>    <chr>               <chr>          <chr>    
#>  1 ITIS:55… Tibetan Babax  english  ITIS:1282110        Babax koslowi  species  
#>  2 ITIS:55… Chinese Babax  english  ITIS:1282108        Babax lanceol… species  
#>  3 ITIS:55… Giant Babax    english  ITIS:1282109        Babax waddelli species  
#>  4 ITIS:55… Spotted Croci… english  ITIS:1282057        Crocias albon… species  
#>  5 ITIS:55… Grey-crowned … english  ITIS:1282056        Crocias langb… species  
#>  6 ITIS:56… Black-faced L… english  ITIS:916118         Garrulax affi… species  
#>  7 ITIS:56… White-throate… english  ITIS:1282111        Garrulax albo… species  
#>  8 ITIS:56… Brown-capped … english  ITIS:916113         Garrulax aust… species  
#>  9 ITIS:56… White-speckle… english  ITIS:1282091        Garrulax bieti species  
#> 10 ITIS:56… Nilgiri Laugh… english  ITIS:1282059        Garrulax cach… species  
#> # ℹ more rows
#> # ℹ 9 more variables: taxonomicStatus <chr>, kingdom <chr>, phylum <chr>,
#> #   class <chr>, order <chr>, family <chr>, genus <chr>, specificEpithet <chr>,
#> #   infraspecificEpithet <chr>

# }
```
