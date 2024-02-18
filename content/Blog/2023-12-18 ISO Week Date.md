---
title: ISO Week Date
date: 2023-12-18
---
As I work on querying fitness activities I've done each day and sum them by week ([[Fitness Software and Projects]]) I thought, hey, use ISO week, there are built in functions in Golang for this...

For a while I wanted the beginning day of week instead of just using something like `2023-W51`. I was thinking this would be Sunday that the day is a part of. Come to find out for December: the set week starts are: 06, 13, 20, 27.  I've obviously never messed with ISO weeks before. Dates aren't the most fun, but learned something with [Wikipedia's help](https://en.wikipedia.org/wiki/ISO_week_date#Dates_with_fixed_week_number).

**Google Searches**
* [ISO 8601 - Wikipedia](https://en.wikipedia.org/wiki/ISO_8601)
* [Go - Unix timestamp for first day of the week from ISO year week - Stack Overflow](https://stackoverflow.com/questions/18624177/go-unix-timestamp-for-first-day-of-the-week-from-iso-year-week)
* [Golang Time in UTC, PST, and EST - Golang Docs](https://golangdocs.com/golang-time-in-utc-pst-est)
* [Golang Int To String Conversion Example | Golang Cafe](https://golang.cafe/blog/golang-int-to-string-conversion-example.html)