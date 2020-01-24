# PredB.me RSS feed Parser

[![Build Status](https://travis-ci.org/luckylittle/predb_me_rss_parser.svg?branch=master)](https://travis-ci.org/luckylittle/predb_me_rss_parser)
[![GitHub license](https://img.shields.io/github/license/luckylittle/predb_me_rss_parser.svg)](https://github.com/luckylittle/predb_me_rss_parser/blob/master/LICENSE)
[![Version](https://img.shields.io/badge/Version-0.0.1-green.svg)](https://github.com/luckylittle/predb_me_rss_parser/releases)
[![Go Report Card](https://goreportcard.com/badge/github.com/luckylittle/predb_me_rss_parser)](https://goreportcard.com/report/github.com/luckylittle/predb_me_rss_parser)


[Golang](https://golang.org/) implementation of the [RSS feed](https://en.wikipedia.org/wiki/RSS) parser explicitly for the [PreDB.me](https://predb.me/) website (uses minimal Atom 2.0 feed type without pub date).

## Technical details

1. HTTP GET https://predb.me/?rss=1
![xml_document_tree.png](img/xml_document_tree.png)
2. Transform `<rss xmlns:atom="http://www.w3.org/2005/Atom" version="2.0"> ... </rss>` into XML struct:
   - 1x top item `<channel> ... </channel>` contains
   - 40x nested `<item> ... </item>` items which each contain
   - 1x `<title> ... </title>` for each item
3. Create a list of the 40 titles, while caching the information of the latest title (first `<title>` is the latest)
4. Run steps 1.-3. every `X` minutes

## Note:

As a backup, similar RSS feed https://predb.ovh/api/v1/rss can be used, or for searching REST API https://predb.ovh/api/v1/?q=foobar can also be used.

---

_Last update: Thu Jan 23 23:52:43 UTC 2020_
