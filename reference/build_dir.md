# Where build inputs and outputs are kept

Where build inputs and outputs are kept

## Usage

``` r
build_dir()
```

## Value

path to the taxadb build directory

## Details

Provider archives are large and slow to fetch, so they are cached here
between builds. Override with the `TAXADB_BUILD_DIR` environment
variable.

## Examples

``` r
build_dir()
#> [1] "/github/home/.cache/R/taxadb/build"
```
