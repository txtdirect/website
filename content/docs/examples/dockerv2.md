+++
fragment = "content"
disabled = true
weight = 300

title = "Dockerv2"

[sidebar]
  enable = true
+++

## Dockerv2
**Dockerv2 based vanity redirect**  
*container.example.com -> hub.example.com/some/container*
```
container.example.com             3600 IN CNAME  txtdirect.example.com
_redirect.container.example.com   3600 IN TXT    "v=txtv0;https://hub.example.com/some/container;type=dockerv2"
```
