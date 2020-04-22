+++
fragment = "content"
weight = 100

title = "Host"

[sidebar]
  enable = true
+++

**Host redirect using default redirection code**  
_example.com -> about.example.com 301_

```
example.com                   3600 IN A      127.0.0.1
_redirect.example.com         3600 IN TXT    "v=txtv0;type=host;to=https://about.example.com"
```

**Host redirect using explicit 301 redirection code**  
_www.example.com -> about.example.com 301_

```
www.example.com               3600 IN CNAME  txtdirect.example.com.
_redirect.www.example.com     3600 IN TXT    "v=txtv0;type=host;code=301;to=https://about.example.com"
```

**Host redirect using explicit 302 redirection code**  
_www.example.com -> about.example.com 302_

```
www.example.com               3600 IN CNAME  txtdirect.example.com.
_redirect.www.example.com     3600 IN TXT    "v=txtv0;type=host;code=302;to=https://about.example.com"
```

**Host redirect using placeholder**  
_example.com -> about.example.com 301_

```
example.com                   3600 IN A      127.0.0.1
_redirect.example.com         3600 IN TXT    "v=txtv0;type=host;to=https://about.example.com{uri}"
```

**Host redirect using multiple placeholders**  
_placeholder.example.com/cat.png -> example.com/cat.png_

```
placeholder.example.com              3600 IN CNAME  txtdirect.example.com.
_redirect.placeholder.example.com    3600 IN TXT    "v=txtv0;type=host;to=https://example.com/{path}{file}"
```
