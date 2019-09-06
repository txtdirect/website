+++
fragment = "content"
weight = 100

title = "Configuration"

[sidebar]
  enable = true
  sticky = true
+++

# Redirect Types

---

## Supported redirect types

| Type Name | Type Description                                            |
| --------- | ----------------------------------------------------------- |
| www       | Redirect all requests to "www"-subdomain                    |
| host      | Redirect to host provided in TXT record                     |
| path      | Enable path based redirects                                 |
| gometa    | Enable Go package meta/vanity redirects                     |
| dockerv2  | Redirect to docker registry or image provided in TXT record |
| proxy     | Proxy the request to endpoint provided in TXT record        |

---

## Enable single type

```
txtdirect {
  enable www
}
```

## Enable multiple types

```
txtdirect {
  enable host path gometa dockerv2
}
```

## Disable specific type

```
txtdirect {
  disable www
}
```

# Fallback

---

## Flow

Step-by-Step fallback flow:

- Current TXT record's `to=` field
- Current TXT record's `website=` field
- Current TXT record's `root=` field
- Parent (type=path) TXT record's `website=` field
- Parent (type=path) TXT record's `root=` field
- Parent (type=path) TXT record's `to=` field
- Request's host "www"-subdomain (if enabled)
- Global config's `redirect` field (if configured)
- 404 Status code

## Global fallback config

### Enable "www"-subdomain fallback

```
txtdirect {
  enable www
}
```

### Default `redirect` fallback

```
txtdirect {
  redirect https://example.com
}
```

# Prometheus Metrics

---

## Metrics name

| Metric Name                           | Metric Description                         |
| ------------------------------------- | ------------------------------------------ |
| txtdirect_redirect_count_total        | Total requests per host                    |
| txtdirect_redirect_status_count_total | Total returned statuses per host           |
| txtdirect_redirect_type_count_total   | Total requests for each host based on type |
| txtdirect_fallback_type_count_total   | Total fallbacks triggered for each type    |
| txtdirect_redirect_path_count_total   | Total redirects per path for each host     |

## Prometheus config

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

# QR

---

By enabling QR, if the incoming request has a "?qr" query, TXTDirect will serve the request's URI QR code.

## Config

By providing additional configs like size, background color, and foreground color you can configure how the generated QR codes look.

### Enable QR

```
txtdirect {
  qr
}
```

### Advanced config

```
txtdirect {
  qr {
    size 512
    background #ffffff
    foreground #000000
  }
}
```

# DNS Resolver

---

To use a custom DNS resolver instead of the machine's default resolver, you can provide the `resolver` address in the config.

## Config

```
txtdirect {
  resolver 127.0.0.1:5353
}
```
