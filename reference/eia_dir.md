# EIA directory

Obtain EIA directory listing.

## Usage

``` r
eia_dir(dir = NULL, tidy = TRUE, cache = TRUE, key = eia_get_key())
```

## Arguments

- dir:

  character, directory path, if `NULL` then the API root directory.

- tidy:

  logical, return a tidier result. See details.

- cache:

  logical, cache result for duration of R session using memoization. See
  details.

- key:

  API key: character if set explicitly; not needed if key is set
  globally. See
  [`eia_set_key()`](https://docs.ropensci.org/eia/reference/eia_key.md).

## Value

data frame, list, or character; see details.

## Details

By default, additional processing is done to return a list containing
tibble data frames. Set `tidy = FALSE` to return only the initial list
result of
[`jsonlite::fromJSON()`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html).
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
# use eia_set_key() to store API key
eia_dir()
eia_dir("electricity")
eia_dir("electricity/rto")
} # }
```
