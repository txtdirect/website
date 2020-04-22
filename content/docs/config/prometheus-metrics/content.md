+++
fragment = "content"
weight = 200

title = "Prometheus Metrics"

[sidebar]
  enable = true
  sticky = true
+++

# Metrics Labels

---

| Label Name | Label Description                                 |
| ---------- | ------------------------------------------------- |
| {host}     | Host name in request's URI                        |
| {path}     | Path in request's URI                             |
| {type}     | Record Type (host, path, proxy, dockerv2, gometa) |
| {fallback} | Fallback Type (global, to, website, root)         |
| {status}   | Response's status code                            |

# Prometheus config

---

You can either use the default settings for enabling Prometheus metrics or the advanced config to provide a custom address and path for exporting metrics.

### Enable Prometheus metrics

```
txtdirect {
  prometheus
}
```

### Advanced config

```
txtdirect {
  prometheus {
    address 192.168.0.1:6543
    path /mymetrics
  }
}
```
