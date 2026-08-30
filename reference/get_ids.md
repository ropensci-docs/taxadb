# get_ids

A drop-in replacement for `[taxize::get_ids()]`

## Usage

``` r
get_ids(
  names,
  provider = getOption("taxadb_default_provider", "itis"),
  format = c("prefix", "bare", "uri"),
  version = latest_version(),
  taxadb_db = td_connect(),
  ignore_case = FALSE,
  warn = TRUE,
  db = NULL,
  ...
)
```

## Arguments

- names:

  a list of scientific names (which may include higher-order ranks in
  most authorities).

- provider:

  abbreviation code for the provider. See details.

- format:

  Format for the returned identifier, one of

  - `prefix` (e.g. `NCBI:9606`, the default), or

  - `bare` (e.g. `9606`, used in `taxize::get_ids()`),

  - `uri` (e.g. `http://ncbi.nlm.nih.gov/taxonomy/9606`).

- version:

  Which version of the taxadb provider database should we use? defaults
  to latest. see `[avialable_releases()]` for details.

- taxadb_db:

  Connection to from `[td_connect()]`.

- ignore_case:

  should we ignore case (capitalization) in matching names? default is
  `TRUE`.

- warn:

  should we display warnings on NAs resulting from multiply-resolved
  matches? (Unlike unmatched names, these NAs can usually be resolved
  manually via
  [`filter_id()`](https://docs.ropensci.org/taxadb/reference/filter_id.md))

- db:

  previous name for `provider` argument, now deprecated

- ...:

  additional arguments (currently ignored)

## Value

a vector of IDs, of the same length as the input names Any unmatched
names or multiply-matched names will return as
[NA](https://rdrr.io/r/base/NA.html)s. To resolve multi-matched names,
use `[filter_name()]` instead to return a table with a separate row for
each separate match of the input name.

## Details

Note that some taxize authorities: `nbn`, `tropicos`, and `eol`, are not
recognized by taxadb and will throw an error here. Meanwhile, taxadb
recognizes several authorities not known to `[taxize::get_ids()]`. Both
include `itis`, `ncbi`, `col`, and `gbif`.

Like all taxadb functions, this function will run fastest if a local
copy of the provider is installed in advance using `[td_create()]`.

## See also

filter_name

Other get:
[`get_names()`](https://docs.ropensci.org/taxadb/reference/get_names.md)

## Examples

``` r
# \donttest{


get_ids("Midas bicolor")
#> Joining with `by = join_by(scientificName)`
#> [1] "ITIS:572923"
get_ids(c("Midas bicolor", "Homo sapiens"), format = "prefix")
#> Joining with `by = join_by(scientificName)`
#> [1] "ITIS:572923" "ITIS:180092"
get_ids("Midas bicolor", format = "uri")
#> Joining with `by = join_by(scientificName)`
#> [1] "http://www.itis.gov/servlet/SingleRpt/SingleRpt?search_topic=TSN&search_value=572923"

# }

```
