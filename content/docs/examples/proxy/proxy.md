+++
fragment = "content"
weight = 500

title = "Proxy"

[sidebar]
  enable = true
+++

Note: **This type is in experimental state**

**Proxy requests to the specified upstream**  
_example.com -> about.example.com_

```
example.com                   3600 IN A      127.0.0.1
_redirect.example.com         3600 IN TXT    "v=txtv0;type=proxy;to=https://about.example.com"
```
