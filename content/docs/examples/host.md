+++
fragment = "content"
weight = 100

title = "Host"

[sidebar]
  enable = true
+++

## Host Type
**Host redirect using default redirection code**  
*example.com -> about.example.com 301*
```
example.com                   3600 IN A      127.0.0.1
_redirect.example.com         3600 IN TXT    "v=txtv0;to=https://about.example.com;type=host"
```

**Host redirect using explicit 301 redirection code**  
*www.example.com -> about.example.com 301*
```
www.example.com               3600 IN CNAME  txtdirect.example.com.
_redirect.www.example.com     3600 IN TXT    "v=txtv0;to=https://about.example.com;type=host;code=301"
```

**Host redirect using explicit 302 redirection code**  
*www.example.com -> about.example.com 302*
```
www.example.com               3600 IN CNAME  txtdirect.example.com.
_redirect.www.example.com     3600 IN TXT    "v=txtv0;to=https://about.example.com;type=host;code=302"
```

**Host redirect using placeholder**  
*example.com -> about.example.com 301*
```
example.com                   3600 IN A      127.0.0.1
_redirect.example.com         3600 IN TXT    "v=txtv0;to=https://about.example.com{uri};type=host"
```

**Host redirect using multiple placeholders**  
*placeholder.example.com/cat.png -> example.com/cat.png*
```
placeholder.example.com              3600 IN CNAME  txtdirect.example.com.
_redirect.placeholder.example.com    3600 IN TXT    "v=txtv0;to=https://example.com/{path}{file};type=host"
```
