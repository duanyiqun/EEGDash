# eegdash.dataset.snapshot module

Single data-access seam for the docs build.

One server `chart-data` call (rows + montages + metadata, all shaped
server-side) with disk-cache and package-CSV fallbacks, self-reporting
provenance via `DatasetSnapshot.source`.

<!-- !! processed by numpydoc !! -->

### *class* eegdash.dataset.snapshot.DatasetSnapshot(, rows: [DataFrame](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html#pandas.DataFrame), aggregations: [dict](https://docs.python.org/3/library/stdtypes.html#dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Any](https://docs.python.org/3/library/typing.html#typing.Any)], montages: [Mapping](https://docs.python.org/3/library/typing.html#typing.Mapping)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Mapping](https://docs.python.org/3/library/typing.html#typing.Mapping)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Any](https://docs.python.org/3/library/typing.html#typing.Any)]], source: [Literal](https://docs.python.org/3/library/typing.html#typing.Literal)['live', 'cached', 'package-csv'], fetched_at: [datetime](https://docs.python.org/3/library/datetime.html#datetime.datetime), api_errors: [list](https://docs.python.org/3/library/stdtypes.html#list)[[str](https://docs.python.org/3/library/stdtypes.html#str)] | [None](https://docs.python.org/3/library/constants.html#None) = None, manifest: [dict](https://docs.python.org/3/library/stdtypes.html#dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Any](https://docs.python.org/3/library/typing.html#typing.Any)] | [None](https://docs.python.org/3/library/constants.html#None) = None, metadata: [Mapping](https://docs.python.org/3/library/typing.html#typing.Mapping)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Mapping](https://docs.python.org/3/library/typing.html#typing.Mapping)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Any](https://docs.python.org/3/library/typing.html#typing.Any)]] | [None](https://docs.python.org/3/library/constants.html#None) = None)

Bases: [`object`](https://docs.python.org/3/library/functions.html#object)

A frozen view of the dataset catalog for one docs build.

Build with `build()`, read via the accessors; provenance on
`source` / `fetched_at` / `api_errors`.

<!-- !! processed by numpydoc !! -->

#### aggregations() → [dict](https://docs.python.org/3/library/stdtypes.html#dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Any](https://docs.python.org/3/library/typing.html#typing.Any)]

Server-side totals; empty on a fallback (cached / package-csv) build.

<!-- !! processed by numpydoc !! -->

#### api_errors *: [list](https://docs.python.org/3/library/stdtypes.html#list)[[str](https://docs.python.org/3/library/stdtypes.html#str)]* *= []*

#### *classmethod* build(api_base: [str](https://docs.python.org/3/library/stdtypes.html#str) = 'https://data.eegdash.org/api', database: [str](https://docs.python.org/3/library/stdtypes.html#str) = 'eegdash', , limit: [int](https://docs.python.org/3/library/functions.html#int) | [None](https://docs.python.org/3/library/constants.html#None) = None, force_refresh: [bool](https://docs.python.org/3/library/functions.html#bool) = False) → DatasetSnapshot

Fetch / cache / fallback in one call, memoised per process.

Order: live `chart-data` → disk cache → package CSV (each failure
recorded on `api_errors`). `limit` defaults to
`EEGDASH_DOC_LIMIT` or 1000; `force_refresh` skips both caches.

<!-- !! processed by numpydoc !! -->

#### *property* dataset_count *: [int](https://docs.python.org/3/library/functions.html#int)*

<!-- !! processed by numpydoc !! -->

#### fetched_at *: [datetime](https://docs.python.org/3/library/datetime.html#datetime.datetime) | [None](https://docs.python.org/3/library/constants.html#None)* *= None*

#### manifest *: [dict](https://docs.python.org/3/library/stdtypes.html#dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Any](https://docs.python.org/3/library/typing.html#typing.Any)]* *= {}*

#### metadata(dataset_id: [str](https://docs.python.org/3/library/stdtypes.html#str)) → [Mapping](https://docs.python.org/3/library/typing.html#typing.Mapping)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Any](https://docs.python.org/3/library/typing.html#typing.Any)] | [None](https://docs.python.org/3/library/constants.html#None)

Server metadata dict for one dataset (case-insensitive), or `None`.

Live builds only; cached / package-csv builds carry none.

<!-- !! processed by numpydoc !! -->

#### montage(dataset_id: [str](https://docs.python.org/3/library/stdtypes.html#str)) → [Mapping](https://docs.python.org/3/library/typing.html#typing.Mapping)[[str](https://docs.python.org/3/library/stdtypes.html#str), [Any](https://docs.python.org/3/library/typing.html#typing.Any)] | [None](https://docs.python.org/3/library/constants.html#None)

Top montage dict for one dataset (case-insensitive), or `None`.

<!-- !! processed by numpydoc !! -->

#### rows() → [DataFrame](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html#pandas.DataFrame)

Per-dataset records as a DataFrame (a copy, so callers can’t leak state).

<!-- !! processed by numpydoc !! -->

#### *property* schema_version *: [str](https://docs.python.org/3/library/stdtypes.html#str) | [None](https://docs.python.org/3/library/constants.html#None)*

Server `schema_version` from the manifest, or `None`.

<!-- !! processed by numpydoc !! -->

#### source *: [Literal](https://docs.python.org/3/library/typing.html#typing.Literal)['live', 'cached', 'package-csv']* *= 'package-csv'*
