+++
fragment = "content"
weight = 200

title = "Path"

[sidebar]
  enable = true
+++

**Path redirect using default ordering**  
_example.com/firstMatch/secondMatch -> about.example.com_
_example.com/firstMatch/noMatch -> fallback or 404_

```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;type=host;to=https://about.example.com/"
```

**Path redirect using explicit ordering**  
_example.com/firstMatch/secondMatch -> about.example.com_
_example.com/firstMatch/noMatch -> fallback or 404_

```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path;from=/$1/$2/"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;type=host;to=https://about.example.com/"
```

**Path redirect using modified ordering**  
_example.com/firstMatch/secondMatch -> about.example.com_
_example.com/firstMatch/noMatch -> defaults or 404_

```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path;from=/$2/$1/"
_redirect.firstmatch.secondmatch.example.com  3600 IN TXT    "v=txtv0;type=host;to=https://about.example.com/"
```

**Path redirect using path record fallback for root/index**  
_example.com/ -> root.example.com_

```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path;from=/$1/$2;root=https://root.example.com"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;type=host;to=https://about.example.com/"
```

**Path redirect using path record fallback**  
_example.com/firstMatch/noMatch -> fallback.example.com_

```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path;to=https://fallback.example.com"
```

**Path redirect using wildcard**  
_example.com/firstMatch/secondMatch -> about.example.com_
_example.com/firstMatch/randomString -> wildcard.example.com_
_example.com/randomString/randomString -> full-wildcard.example.com_

```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;type=host;to=https://about.example.com/"
_redirect._.firstmatch.example.com            3600 IN TXT    "v=txtv0;type=host;to=https://wildcard.example.com/"
_redirect._._.example.com                     3600 IN TXT    "v=txtv0;type=host;to=https://full-wildcard.example.com/"
```

<!--


*example.com/firstMatch/secondMatch -> about.example.com*
*example.com/firstMatch/noMatch -> fallback.example.com*
```
example.com                                   3600 IN A      127.0.0.1
_redirect.example.com                         3600 IN TXT    "v=txtv0;type=path;re=\/(.*)\/(.*);to=https://fallback.example.com"
_redirect.secondmatch.firstmatch.example.com  3600 IN TXT    "v=txtv0;type=host;to=https://about.example.com"
```

-->
