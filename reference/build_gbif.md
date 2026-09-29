# Rebuild the GBIF backbone snapshot

Rebuild the GBIF backbone snapshot

## Usage

``` r
build_gbif(
  version = format(Sys.Date(), "%Y"),
  archive = NULL,
  dir = build_dir(),
  db = td_connect()
)
```

## Arguments

- version:

  snapshot version to write, e.g. `"2026"`

- archive:

  path to the GBIF backbone archive; downloaded if missing

- dir:

  directory for build inputs and outputs

- db:

  a duckdb connection

## Value

the paths written, invisibly

## Details

GBIF supplies `canonicalName` – the name without authorship – alongside
the full `scientificName`, so no name parsing is needed. It leaves
`canonicalName` empty for names its parser cannot analyse, which
includes the sequence-derived identifiers GBIF carries in quantity (BOLD
BINs, UNITE species hypotheses, metagenome-assembled genomes) and hybrid
formulas; for those the `scientificName` is the name, and is used.

GBIF leaves `acceptedNameUsageID` empty on `accepted` and on `doubtful`
names alike, since it redirects neither. Both therefore become their own
accepted name here, which is also what keeps GBIF's 40,895 synonyms of
doubtful names resolvable.

## See also

Other build:
[`build_col()`](https://docs.ropensci.org/taxadb/reference/build_col.md),
[`build_fishbase()`](https://docs.ropensci.org/taxadb/reference/build_fishbase.md),
[`build_itis()`](https://docs.ropensci.org/taxadb/reference/build_itis.md),
[`build_ncbi()`](https://docs.ropensci.org/taxadb/reference/build_ncbi.md),
[`build_ott()`](https://docs.ropensci.org/taxadb/reference/build_ott.md)

## Examples

``` r
if (FALSE) { # \dontrun{
build_gbif("2026")
} # }
```
