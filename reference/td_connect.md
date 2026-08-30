# Connect to the taxadb database

Connect to the taxadb database

## Usage

``` r
td_connect(dbdir = NULL, driver = NULL, read_only = NULL)
```

## Arguments

- dbdir:

  Deprecated, ignored.

- driver:

  Deprecated, ignored. The driver is always `duckdb`.

- read_only:

  Deprecated, ignored.

## Value

a DBI `connection` to an in-process duckdb database, configured for
anonymous streaming reads from the `taxadb` data repository.

## Details

`taxadb` reads Parquet snapshots directly from object storage
(<https://source.coop>) using `duckdb`'s `httpfs` extension, so no data
import step is required. This function returns a connection with
`httpfs` loaded and the S3 endpoint configured for anonymous access.

For performance reasons the connection is cached and reused, making
repeated calls to `td_connect()` much faster and more failsafe than
repeated calls to
[DBI::dbConnect](https://dbi.r-dbi.org/reference/dbConnect.html).

The `httpfs` extension needed for remote reads is loaded on first use
rather than at connect time, so a session that only reads local
snapshots or the bundled test data never touches the network.

`duckdb` would otherwise scan with one thread per core and let its
buffer pool grow to most of system RAM. For the selective scans `taxadb`
makes that is the wrong trade: each scanning thread holds a decompressed
Parquet row group, so memory grows with core count while the query gets
no faster. On a 128-core machine, looking up one name in the GBIF table
peaked at 1324 MB with the duckdb defaults and 322 MB capped at eight
threads – and the capped run was faster (0.7s against 1.0s).

So the connection caps threads at `TAXADB_THREADS` (8) or the core
count, whichever is lower. Raise it with `options(taxadb_threads=)` for
bulk work –
[`td_build()`](https://docs.ropensci.org/taxadb/reference/td_build.md)
does this itself – and set `options(taxadb_memory_limit=)` to bound the
buffer pool.

## Examples

``` r
# \donttest{
db <- td_connect()
# }
```
