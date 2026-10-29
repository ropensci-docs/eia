# Set and get API key

Set and get API key

## Usage

``` r
eia_set_key(key, store = c("env", "options", "sysenv"))

eia_get_key(store = c("env", "options", "sysenv"))
```

## Arguments

- key:

  character, API key.

- store:

  character, method for storing API key. See details.

## Value

`eia_get_key()` returns the key string or `NULL` with a warning.
`eia_set_key()` returns a success message or an error.

## Details

Setter and getter helpers allow you to store your EIA API key in one of
three ways. Their use is optional. You can always pass the API key
string to the `key` argument of any package function that requires it,
but you do not have to.

By default the `key` argument for these functions is
`key = eia_get_key()`. If your key has been stored in a manner that can
be retrieved, then you can call all the package API functions without
having to provide the `key` argument repeatedly.

## Key storage methods

If you have already set your key globally somewhere using
`eia_set_key()`, `eia_get_key()` will retrieve it. You can add the
`EIA_KEY = "yourkey"` key-value pair to
[`options()`](https://rdrr.io/r/base/options.html) or as a system
environment variable yourself and `eia_get_key()` will pick it up as
long as you use the name `EIA_KEY`. For convenience you can do this in
your R session with `eia_set_key()`. It gives you three options for how
to store the key. The default is to use the `eia` package environment
that is created when the package is loaded.

## Precedence

Choose one method when setting a key. When getting the key, the three
locations are checked in the order: package environment,
[`options()`](https://rdrr.io/r/base/options.html), then the system
environment. To override the order, specify the method explicitly and
the check will only occur there. This also makes it possible to override
a system level key by working with one stored in the package environment
or [`options()`](https://rdrr.io/r/base/options.html).

## Persistence

Note that none of these three storage methods, including `"sysenv"` are
persistent; the stored key is lost when the R session is terminated. A
key that is stored outside of R as a system environment variable is
retrievable with `eia_get_key()`, just like those set in an R session
with `eia_set_key()` and `store = "sysenv"`. However, if you truly want
the key to persist as an environment variable when R terminates, you
must manually add it somewhere like `.Renviron`; `Sys.setenv` in R
cannot achieve this.

## Examples

``` r
eia_set_key("fake")
#> Key stored successfully in package environment.
eia_get_key()
#> [1] "fake"
# eia_get_key("options") # `NULL` with warning if not set where specified
```
