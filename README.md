# PredB.me RSS feed Parser

[Golang](https://golang.org/) implementation of the [RSS feed](https://en.wikipedia.org/wiki/RSS) parser explicitly for the [PreDB.me](https://predb.me/) website (uses minimal Atom 2.0 feed type without pub date).

## Technical details

1. HTTP GET https://predb.me/?rss=1
2. Transform `<rss xmlns:atom="http://www.w3.org/2005/Atom" version="2.0"> ... </rss>` into XML struct:
   - 1x top item `<channel> ... </channel>` contains
   - 40x nested `<item> ... </item>` items which each contain
   - 1x `<title> ... </title>`
3. Create a list of the 40 titles, while caching the information of the latest title (first `<title>` is the latest)
4. Run steps 1.-3. every `X` minutes

---

_Last update: Wed Jan  8 23:46:44 UTC 2020_
