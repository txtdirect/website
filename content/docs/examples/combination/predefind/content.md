+++
fragment = "content"
weight = 100

title = "Predefined Regex"

[sidebar]
  enable = true
+++

The `path` type has a feature called predefined regex that basically reads the
`re=` field of the child zones and choses the record with most specific regex
match. This feature enables you to have more advanced redirects and use
different regexes in subzones to easily separate complex logics for `path`
redirects.

When a `path` record contains a `re=` field and its value is `record`, TXTDirect
will look for a list of numbered subzones that start from **1** and matches the
request's path with each of these records' `re=` field to find the most specific
match. Take a look at the example below:

```
"_redirect.example.com.":     "v=txtv0;re=record;to=https://example.com;type=path",
"_redirect.1.example.com.":   "v=txtv0;re=\\/test1;to=https://example.com/first/predefined{1};type=host",
"_redirect.2.example.com.":   "v=txtv0;re=\\/test1\\/test2;to=https://example.com/second/predefined{1};type=host",
```

In the example above we have a `path` record which is `_redirect.example.com`
and its `re=` field is set to `record`. When a request comes for `example.com`,
TXTDirect looks for the numbered subdomains which start from
`_redirect.1.example.com`. Then TXTDirect will match the request's path with the
subzons `re=` field to find the most specific
match. After finding the match, it will use that record to redirect the request.
Which in this case if the incoming request's path is `/test1/test2`, TXTDirect
will use the `_redirect.2.example.com` record and after parsing the placeholders,
redirects the request to `https://example.com/second/predefined/test1/test2`.

For more information about the `path` records check the
[Specification](/docs/specification/#path-type) page and for a list of
placeholders and their description check the [Placeholders](/docs/placeholders)
page.
