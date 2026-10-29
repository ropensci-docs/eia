# Clear API results cache

Reset the results of API calls that are currently cached in memory.

## Usage

``` r
eia_clear_cache()

eia_clear_dir()

eia_clear_metadata()

eia_clear_data()

eia_clear_facets()
```

## Details

`eia_clear_cache()` clears the entire cache. The other functions clear
the cache associated with specific endpoints.

## Examples

``` r
if (FALSE) { # \dontrun{
key <- Sys.getenv("EIA_KEY") # your stored API key
system.time(eia_dir(key))
system.time(eia_dir(key))
eia_clear_cache()
system.time(eia_dir(key))
} # }
```
