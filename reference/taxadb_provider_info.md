# Describe the taxonomic name providers

Describe the taxonomic name providers

## Usage

``` r
taxadb_provider_info(provider = taxadb_providers())
```

## Arguments

- provider:

  one or more provider abbreviations; all by default

## Value

a data.frame with one row per provider giving its `title`, `url`, the
`source` its data is taken from, its `license` and a `citation`.

## Details

Providers are not interchangeable. `col`, `gbif` and `ott` are synthesis
projects that integrate other checklists, while `itis`, `ncbi`, `fb` and
`slb` are primary authorities; the `synthesis` column records which is
which. More importantly, providers disagree: the same name can be
accepted by one and a synonym of something else in another, so a name
resolved against one provider should not be mixed with names resolved
against another. See
[`vignette("data-sources")`](https://docs.ropensci.org/taxadb/articles/data-sources.md).

Redistribution terms differ too. `fb` and `slb` are CC BY-NC, so those
two tables may not be used commercially.

## Examples

``` r
taxadb_provider_info()
#>   provider                                   title
#> 1     itis Integrated Taxonomic Information System
#> 2     ncbi                           NCBI Taxonomy
#> 3      col                       Catalogue of Life
#> 4     gbif                  GBIF Backbone Taxonomy
#> 5      ott                      Open Tree Taxonomy
#> 6       fb                                FishBase
#> 7      slb                             SeaLifeBase
#>                                     url
#> 1                  https://www.itis.gov
#> 2 https://www.ncbi.nlm.nih.gov/taxonomy
#> 3       https://www.catalogueoflife.org
#> 4                  https://www.gbif.org
#> 5       https://tree.opentreeoflife.org
#> 6                  https://fishbase.org
#> 7           https://www.sealifebase.org
#>                                                                    source
#> 1                           https://www.itis.gov/downloads/itisSqlite.zip
#> 2                    https://ftp.ncbi.nih.gov/pub/taxonomy/taxdump.tar.gz
#> 3                  https://download.checklistbank.org/col/latest_dwca.zip
#> 4 https://hosted-datasets.gbif.org/datasets/backbone/current/backbone.zip
#> 5                                   https://files.opentreeoflife.org/ott/
#> 6                                              s3://cboettig/fishbase/fb/
#> 7                                             s3://cboettig/fishbase/slb/
#>         license                                        license_url synthesis
#> 1 public domain                 https://www.itis.gov/citation.html     FALSE
#> 2 public domain  https://www.ncbi.nlm.nih.gov/home/about/policies/     FALSE
#> 3     CC BY 4.0       https://creativecommons.org/licenses/by/4.0/      TRUE
#> 4     CC BY 4.0       https://creativecommons.org/licenses/by/4.0/      TRUE
#> 5       CC0 1.0 https://creativecommons.org/publicdomain/zero/1.0/      TRUE
#> 6  CC BY-NC 4.0    https://creativecommons.org/licenses/by-nc/4.0/     FALSE
#> 7  CC BY-NC 4.0    https://creativecommons.org/licenses/by-nc/4.0/     FALSE
#>                                                                                                                                                      citation
#> 1                                                                                        Integrated Taxonomic Information System (ITIS). doi:10.5066/F7KH0KBK
#> 2                     Schoch CL, et al. NCBI Taxonomy: a comprehensive update on curation, resources and tools. Database (2020). doi:10.1093/database/baaa062
#> 3                                                                                          Bánki O, et al. Catalogue of Life. https://www.catalogueoflife.org
#> 4                                                                                   GBIF Secretariat. GBIF Backbone Taxonomy. https://doi.org/10.15468/39omei
#> 5 Rees JA, Cranston K. Automated assembly of a reference taxonomy for phylogenetic data synthesis. Biodiversity Data Journal (2017). doi:10.3897/BDJ.5.e12581
#> 6                                                                                                 Froese R, Pauly D (eds). FishBase. https://www.fishbase.org
#> 7                                                                                      Palomares MLD, Pauly D (eds). SeaLifeBase. https://www.sealifebase.org
taxadb_provider_info("col")$citation
#> [1] "Bánki O, et al. Catalogue of Life. https://www.catalogueoflife.org"
```
