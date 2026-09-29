# EIA date parsing

Helper functions for manipulating and converting between regular
year-month-day date strings and EIA date string notation.

## Usage

``` r
eiadate_to_date(x)

date_to_eiadate(x, date_format = c("A", "Q", "M", "W", "D", "H"))

eiadate_to_date_seq(start, end, weekly = FALSE)
```

## Arguments

- x:

  character, EIA date string; character or date object for regular
  dates. See details.

- date_format:

  EIA date format: "A", "Q", "M", "W", "D", "H". These stand for annual,
  quarterly, monthly, weekly, daily, hourly. See details.

- start:

  start EIA date or date.

- end:

  end EIA date or date.

- weekly:

  logical. See details.

## Details

There is no reason to mix EIA date formats in this context. Functions
that take EIA date strings expect a consistent format. Also, EIA date
formats are parsed automatically from the dates themselves. However,
daily and weekly use the same format. Too avoid ambiguity in
`eia_date_seq()`, daily is assumed; set `weekly = TRUE` to treat as
weekly.

When providing a real date or date string, such as to
`date_to_eiadate()`, dates should be in `YYYY-MM-DD` format, or at least
any format that can be parsed by
[`lubridate::ymd`](https://lubridate.tidyverse.org/reference/ymd.html)
or
[`lubridate::ymd_hms`](https://lubridate.tidyverse.org/reference/ymd_hms.html)
for dates and hourly date times, respectively.

`"LH"` is not a supported date format. Use `"H"`. The API does not
translate the date and time when using `"LH"` anyhow; it simply appends
the date string with the number of hours time difference.

## Examples

``` r
eiadate_to_date(c("2018-03", "2018-04"))
#> [1] "2018-03-01" "2018-04-01"

date_to_eiadate("2018-05-14", "A")
#> [1] "2018"
date_to_eiadate("2018-05-14", "Q")
#> [1] "2018-Q2"
date_to_eiadate("2018-05-14", "M")
#> [1] "2018-05"

(x <- eiadate_to_date_seq("2018-Q1", "2018-Q4"))
#> [1] "2018-01-01" "2018-04-01" "2018-07-01" "2018-10-01"
date_to_eiadate(x, "Q")
#> [1] "2018-Q1" "2018-Q2" "2018-Q3" "2018-Q4"
date_to_eiadate(x, "M")
#> [1] "2018-01" "2018-04" "2018-07" "2018-10"

(x <- eiadate_to_date("2019-01-02T16Z"))
#> [1] "2019-01-02 16:00:00 UTC"
date_to_eiadate(x, "H")
#> [1] "2019-01-02T16Z"
(x <- eiadate_to_date_seq("2019-01-02T16Z", "2019-01-02T19Z"))
#> [1] "2019-01-02 16:00:00 UTC" "2019-01-02 17:00:00 UTC"
#> [3] "2019-01-02 18:00:00 UTC" "2019-01-02 19:00:00 UTC"
date_to_eiadate(x, "H")
#> [1] "2019-01-02T16Z" "2019-01-02T17Z" "2019-01-02T18Z" "2019-01-02T19Z"
```
