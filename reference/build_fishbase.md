# Rebuild the FishBase or SeaLifeBase snapshot

Rebuild the FishBase or SeaLifeBase snapshot

## Usage

``` r
build_fishbase(
  version = format(Sys.Date(), "%Y"),
  provider = c("fb", "slb"),
  fb_version = NULL,
  dir = build_dir(),
  db = td_connect()
)
```

## Arguments

- version:

  snapshot version to write, e.g. `"2026"`

- provider:

  `"fb"` for FishBase or `"slb"` for SeaLifeBase

- fb_version:

  which FishBase snapshot to build from, e.g. `"v26.07"`. Defaults to
  the most recent published.

- dir:

  directory for build inputs and outputs

- db:

  a duckdb connection

## Value

the paths written, invisibly

## Details

FishBase and SeaLifeBase share a schema, and both are already published
as Parquet alongside the taxadb snapshots, so this build reads them over
the network and downloads nothing.

FishBase numbers accepted species (`SpecCode`) and synonyms (`SynCode`)
in two independent sequences, so the same integer means different things
in each: `SpecCode` 1 is *Scyris indica* while `SynCode` 1 is *Alausa
coerulea*. Prefixing both as `FB:1` would make one identifier name two
taxa, which it did in the previously published table – 20,295 FishBase
identifiers and 61,125 SeaLifeBase ones were ambiguous.

Only `SpecCode` is therefore used as the `taxonID`, and synonyms carry a
`NULL` one exactly as they do for NCBI and OTT. Nothing is lost: the
`SynCode` is published in its own `synonymID` column. A consequence is
that a synonym whose `SpecCode` is 0 – not linked to any species record,
1,043 names in FishBase and 7,512 in SeaLifeBase – has nothing to
resolve to and is dropped.

Classification comes from the `families` table. FishBase covers only
fishes, so its phylum and kingdom are constant. SeaLifeBase spans some
sixty phyla across several kingdoms and asserts no kingdom itself, so
`kingdom` is left empty there rather than inferred.

FishBase data is CC-BY-NC (fishbase.org).

## See also

Other build:
[`build_col()`](https://docs.ropensci.org/taxadb/reference/build_col.md),
[`build_gbif()`](https://docs.ropensci.org/taxadb/reference/build_gbif.md),
[`build_itis()`](https://docs.ropensci.org/taxadb/reference/build_itis.md),
[`build_ncbi()`](https://docs.ropensci.org/taxadb/reference/build_ncbi.md),
[`build_ott()`](https://docs.ropensci.org/taxadb/reference/build_ott.md)

## Examples

``` r
if (FALSE) { # \dontrun{
build_fishbase("2026", provider = "fb")
} # }
```
