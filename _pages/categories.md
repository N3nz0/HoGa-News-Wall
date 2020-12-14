---
layout: categories
title: Categories
permalink: /categories
---

import feedparser

rss_url = "https://www.tophotel.de/feed/"

feed = feedparser.parse( rss_url )
items = feed["items"]
for item in items:
    time = item[ "published_parsed" ]
    title = item[ "title" ].encode('gb18030')
    fileName = str(time.tm_year) + '-' + str(time.tm_mon) + '-' + str(time.tm_mday) + '-' + title + '.md'
    fileName = fileName.replace('/', '')
    f = open(fileName,'w')
    value = item["content"][0]['value'].encode('gb18030')
    f.write('---\nlayout: _post\ntitle: ' + title + '\n')
    f.write('''status: publish
published: true
meta:
  _edit_last: "1"
type: post
tags:
---
''')
    f.write(value)
print 'end'
