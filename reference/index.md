# Package index

## All functions

- [`available_providers()`](https://docs.ropensci.org/taxadb/reference/available_providers.md)
  : Name providers available for a given version

- [`available_versions()`](https://docs.ropensci.org/taxadb/reference/available_versions.md)
  : Versions of the taxadb data available

- [`build_col()`](https://docs.ropensci.org/taxadb/reference/build_col.md)
  : Rebuild the Catalogue of Life snapshot

- [`build_dir()`](https://docs.ropensci.org/taxadb/reference/build_dir.md)
  : Where build inputs and outputs are kept

- [`build_fishbase()`](https://docs.ropensci.org/taxadb/reference/build_fishbase.md)
  : Rebuild the FishBase or SeaLifeBase snapshot

- [`build_gbif()`](https://docs.ropensci.org/taxadb/reference/build_gbif.md)
  : Rebuild the GBIF backbone snapshot

- [`build_itis()`](https://docs.ropensci.org/taxadb/reference/build_itis.md)
  : Rebuild the ITIS snapshot

- [`build_ncbi()`](https://docs.ropensci.org/taxadb/reference/build_ncbi.md)
  : Rebuild the NCBI Taxonomy snapshot

- [`build_ott()`](https://docs.ropensci.org/taxadb/reference/build_ott.md)
  : Rebuild the Open Tree Taxonomy snapshot

- [`clean_names()`](https://docs.ropensci.org/taxadb/reference/clean_names.md)
  : Clean taxonomic names

- [`common_contains()`](https://docs.ropensci.org/taxadb/reference/common_contains.md)
  : common name starts with

- [`common_starts_with()`](https://docs.ropensci.org/taxadb/reference/common_starts_with.md)
  : common name starts with

- [`filter_by()`](https://docs.ropensci.org/taxadb/reference/filter_by.md)
  :

  Creates a data frame with column name given by `by`, and values given
  by the vector `x`, and then uses this table to do a filtering join,
  joining on the `by` column to return all rows matching the `x` values
  (scientificNames, taxonIDs, etc).

- [`filter_common()`](https://docs.ropensci.org/taxadb/reference/filter_common.md)
  : Look up taxonomic information by common name

- [`filter_id()`](https://docs.ropensci.org/taxadb/reference/filter_id.md)
  : Return a taxonomic table matching the requested ids

- [`filter_name()`](https://docs.ropensci.org/taxadb/reference/filter_name.md)
  : Look up taxonomic information by scientific name

- [`filter_rank()`](https://docs.ropensci.org/taxadb/reference/filter_rank.md)
  : Get all members (descendants) of a given rank level

- [`fuzzy_filter()`](https://docs.ropensci.org/taxadb/reference/fuzzy_filter.md)
  : Match names that start or contain a specified text string

- [`get_ids()`](https://docs.ropensci.org/taxadb/reference/get_ids.md) :
  get_ids

- [`get_names()`](https://docs.ropensci.org/taxadb/reference/get_names.md)
  : get_names

- [`latest_version()`](https://docs.ropensci.org/taxadb/reference/latest_version.md)
  : The most recent taxadb snapshot version

- [`list_snapshots()`](https://docs.ropensci.org/taxadb/reference/list_snapshots.md)
  : List the taxonomic snapshots available from the taxadb repository

- [`name_contains()`](https://docs.ropensci.org/taxadb/reference/name_contains.md)
  : return all taxa in which scientific name contains the text provided

- [`name_starts_with()`](https://docs.ropensci.org/taxadb/reference/name_starts_with.md)
  : scientific name starts with

- [`taxa_tbl()`](https://docs.ropensci.org/taxadb/reference/taxa_tbl.md)
  : Return a reference to a given table in the taxadb database

- [`taxadb_dir()`](https://docs.ropensci.org/taxadb/reference/taxadb_dir.md)
  : Show the local taxadb directory

- [`taxadb_provider_info()`](https://docs.ropensci.org/taxadb/reference/taxadb_provider_info.md)
  : Describe the taxonomic name providers

- [`taxadb_providers()`](https://docs.ropensci.org/taxadb/reference/taxadb_providers.md)
  : Providers taxadb can rebuild

- [`taxadb_repo()`](https://docs.ropensci.org/taxadb/reference/taxadb_repo.md)
  : The taxadb data repository

- [`taxadb_uri()`](https://docs.ropensci.org/taxadb/reference/taxadb_uri.md)
  : Locate the Parquet files backing a taxadb table

- [`td_build()`](https://docs.ropensci.org/taxadb/reference/td_build.md)
  : Rebuild taxadb snapshots from the providers

- [`td_connect()`](https://docs.ropensci.org/taxadb/reference/td_connect.md)
  : Connect to the taxadb database

- [`td_create()`](https://docs.ropensci.org/taxadb/reference/td_create.md)
  : Create a local taxadb database

- [`td_disconnect()`](https://docs.ropensci.org/taxadb/reference/td_disconnect.md)
  : Disconnect from the taxadb database.

- [`td_download()`](https://docs.ropensci.org/taxadb/reference/td_download.md)
  : Install a local copy of a taxadb snapshot

- [`td_manifest()`](https://docs.ropensci.org/taxadb/reference/td_manifest.md)
  : Describe a built snapshot

- [`td_validate()`](https://docs.ropensci.org/taxadb/reference/td_validate.md)
  : Check a taxadb table against the taxadb Darwin Core rules

- [`td_write_metadata()`](https://docs.ropensci.org/taxadb/reference/td_write_metadata.md)
  : Write the metadata published with a snapshot
