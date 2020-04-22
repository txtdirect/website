+++
fragment = "content"
weight = 100

title = "Path with Path (chaining)"

[sidebar]
  enable = true
+++

A `path` record can be chained to another parent `path` record and can use some of their parent's information like the `re=` field while processing the request. This feature enables you to have
more complex redirects and also control the flow of requests through a set of records chained together.

**Redirect request using chained path records**  
_example.com/projects/x -> projectx.example.com 301_

```
example.com                            3600 IN A      127.0.0.1
_redirect.example.com                  3600 IN TXT    "v=txtv0;type=path"
_redirect.projects.example.com         3600 IN TXT    "v=txtv0;type=path"
_redirect.x.projects.example.com       3600 IN TXT    "v=txtv0;type=host;to=https://projectx.example.com"
```

---

**Note:** If the child `path` record doesn't have a `re=` field but the parent does,
the custom regex from the parent will get used for processing the path.

---

**Redirect request using parent path record's regex**  
_example.com/projects/x -> one.example.com 301_

```
example.com                            3600 IN A      127.0.0.1
_redirect.example.com                  3600 IN TXT    "v=txtv0;type=path;re=[1]"
_redirect.numbers.example.com          3600 IN TXT    "v=txtv0;type=path"
_redirect.1.numbers.example.com        3600 IN TXT    "v=txtv0;type=host;to=https://one.example.com"
```
