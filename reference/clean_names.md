# Clean taxonomic names

A utility to sanitize taxonomic names to increase probability of
resolving names.

## Usage

``` r
clean_names(
  names,
  fix_delim = TRUE,
  binomial_only = TRUE,
  remove_sp = TRUE,
  ascii_only = TRUE,
  lowercase = TRUE,
  remove_punc = FALSE
)
```

## Arguments

- names:

  a character vector of taxonomic names (usually species names)

- fix_delim:

  Should we replace separators `.`, `_`, `-` with spaces? e.g.
  'Homo.sapiens' becomes 'Homo sapiens'. logical, default TRUE.

- binomial_only:

  Attempt to prune name to a binomial name, e.g. Genus and species
  (specific epithet), e.g. `Homo sapiens sapiens` becomes
  `Homo sapiens`. logical, default
  [TRUE](https://rdrr.io/r/base/logical.html).

- remove_sp:

  Should we drop unspecified species epithet designations? e.g.
  `Homo sp.` becomes `Homo` (thus only matching against genus level
  ids). logical, default [TRUE](https://rdrr.io/r/base/logical.html).

- ascii_only:

  should we coerce strings to ascii characters? (see
  [`stringi::stri_trans_general()`](https://rdrr.io/pkg/stringi/man/stri_trans_general.html))

- lowercase:

  should names be coerced to lower-case to provide case-insensitive
  matching?

- remove_punc:

  replace all punctuation but apostrophes with a space, remove
  apostrophes

## Details

Current implementation is limited to handling a few common cases.
Additional extensions may be added later. A goal of the `clean_names`
function is that any modification rule of the name strings be precise,
atomic, and toggle-able, rather than relying on clever but more opaque
rules and arbitrary scores. This utility should always be used with
care, as indiscriminate modification of names may result in successful
but inaccurate name matching. A good pattern is to only apply this
function to the subset of names that cannot be directly matched.

## Examples

``` r
clean_names(c("Homo sapiens sapiens", "Homo.sapiens", "Homo sp."))
#> [1] "homo sapiens" "homo sapiens" "homo"        
```
