# get_names

Translate identifiers into scientific names

## Usage

``` r
get_names(
  id,
  provider = getOption("taxadb_default_provider", "itis"),
  version = latest_version(),
  format = c("guess", "prefix", "bare", "uri"),
  taxadb_db = td_connect(),
  db = NULL
)
```

## Arguments

- id:

  a list of taxonomic identifiers.

- provider:

  abbreviation code for the provider. See details.

- version:

  Which version of the taxadb provider database should we use? defaults
  to latest. see `[avialable_releases()]` for details.

- format:

  Format for the returned identifier, one of

  - `prefix` (e.g. `NCBI:9606`, the default), or

  - `bare` (e.g. `9606`, used in `taxize::get_ids()`),

  - `uri` (e.g. `http://ncbi.nlm.nih.gov/taxonomy/9606`).

- taxadb_db:

  Connection to from `[td_connect()]`.

- db:

  previous name for `provider` argument, now deprecated

## Value

a vector of names, of the same length as the input ids. Any unmatched
IDs will return as [NA](https://rdrr.io/r/base/NA.html)s.

## Details

Like all taxadb functions, this function will run fastest if a local
copy of the provider is installed in advance using `[td_create()]`.

## See also

Other get:
[`get_ids()`](https://docs.ropensci.org/taxadb/reference/get_ids.md)

## Examples

``` r
# \donttest{


get_names(c("ITIS:1025094", "ITIS:1025103"), format = "prefix")
#> [1] "Leontopithecus fuscus" "Midas bicolor"        

# }
```
