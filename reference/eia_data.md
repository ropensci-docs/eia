# EIA data

Obtain data from the EIA.

## Usage

``` r
eia_data(
  dir,
  data = NULL,
  facets = NULL,
  freq = NULL,
  start = NULL,
  end = NULL,
  sort = NULL,
  length = NULL,
  offset = NULL,
  tidy = TRUE,
  check_metadata = FALSE,
  cache = TRUE,
  key = eia_get_key()
)
```

## Arguments

- dir:

  character, directory path.

- data:

  character or `NULL`,

  - note: if `NULL`, `eia_data()` will only return column headings; must
    input a character value as provided by
    [`eia_metadata()`](https://docs.ropensci.org/eia/reference/eia_metadata.md)
    for data to be returned.

  - see details.

- facets:

  character list or `NULL`, see details.

- freq:

  character or `NULL`, see details.

- start, end:

  character or `NULL`, see details.

- sort:

  named list of two.

  - `cols`: list column names on which to sort.

  - `order`: `"asc"` or `"desc"` for ascending or descending,
    respectively.

- length:

  numeric or `NULL`, number of rows to return.

- offset:

  numeric or `NULL`, number of rows to skip before return.

- tidy:

  logical or `NULL`, return a tidier result. See details.

- check_metadata:

  logical, if `TRUE` checks input values against metadata endpoint.

- cache:

  logical, cache result for duration of R session using memoization. See
  details.

- key:

  API key: character if set explicitly; not needed if key is set
  globally. See
  [`eia_set_key()`](https://docs.ropensci.org/eia/reference/eia_key.md).

## Value

data frame

## Details

By default, `data`, `facets`, and `freq` are set to `NULL`. To obtain
valid input values for each of these arguments, use the specific ID
labels as provided by
[`eia_metadata()`](https://docs.ropensci.org/eia/reference/eia_metadata.md).

The use of `start` and `end` require some input to `freq`. By default
(`check_metadata = FALSE`), the resulting data will match the temporal
resolution provided to `freq`, however, `check_metadata = TRUE` applies
further restrictions such that the format of values provided to
`start`/`end` must match that of `freq`. Furthermore, regardless of the
input format provided to `start`/`end`, the resulting data will always
match the specification of `freq`. And lastly, regardless of chosen
format, `end` must be strictly greater than `start` to return data.

By default, additional processing is done to return a list containing
tibble data frames. Set `tidy = FALSE` to return only the initial list
result of
[`jsonlite::fromJSON`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html).
Set `tidy = NA` to return the original JSON as a character string.

Set to `cache = FALSE` to force a new API call for updated data. Using
`FALSE` always makes a new API call and returns the result from the
server. `TRUE` uses memoization on a per R session basis, caching the
result of the function call in memory for the duration of the R session.
You can reset the entire cache by calling
[`eia_clear_cache()`](https://docs.ropensci.org/eia/reference/eia_clear_cache.md).

## Examples

``` r
if (FALSE) { # \dontrun{
eia_data(
  dir = "electricity/retail-sales",
  data = "price",
  facets = list(sectorid = c("COM", "RES"), stateid = "OH")
)
} # }
```
