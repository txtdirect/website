+++
fragment = "content"
weight = 200

title = "Path"

[sidebar]
  enable = true
+++

## Path Type
**Path redirect using default ordering**  
*example.com/firstMatch/secondMatch -> about.example.com*
*example.com/firstMatch/noMatch -> fallback or 404*
```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;to=https://about.example.com/;type=host"
```

**Path redirect using explicit ordering**  
*example.com/firstMatch/secondMatch -> about.example.com*
*example.com/firstMatch/noMatch -> fallback or 404*
```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;from=/$1/$2/;type=path"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;to=https://about.example.com/;type=host"
```

**Path redirect using modified ordering**  
*example.com/firstMatch/secondMatch -> about.example.com*
*example.com/firstMatch/noMatch -> defaults or 404*
```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;from=/$2/$1/;type=path"
_redirect.firstmatch.secondmatch.example.com  3600 IN TXT    "v=txtv0;to=https://about.example.com/;type=host"
```

**Path redirect using path record fallback for root/index**  
*example.com/ -> root.example.com*
```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;from=/$1/$2;root=https://root.example.com;type=path"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;to=https://about.example.com/;type=host"
```

**Path redirect using path record fallback**  
*example.com/firstMatch/noMatch -> fallback.example.com*
```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;to=https://fallback.example.com;type=path"
```

**Path redirect using wildcard**  
*example.com/firstMatch/secondMatch -> about.example.com*
*example.com/firstMatch/randomString -> wildcard.example.com*
*example.com/randomString/randomString -> full-wildcard.example.com*

```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;to=https://about.example.com/;type=host"
_redirect._.firstmatch.example.com            3600 IN TXT    "v=txtv0;to=https://wildcard.example.com/;type=host"
_redirect._._.example.com                     3600 IN TXT    "v=txtv0;to=https://full-wildcard.example.com/;type=host"
```

<!--


*example.com/firstMatch/secondMatch -> about.example.com*
*example.com/firstMatch/noMatch -> fallback.example.com*
```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;re=\/(.*)\/(.*);to=https://fallback.example.com;type=path"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;to=https://about.example.com;type=host"
```

-->
