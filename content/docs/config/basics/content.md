+++
fragment = "content"
weight = 200

title = "Basics"

[sidebar]
  enable = true
  sticky = true
+++

# Configuring types

---

Enable a single type:

```
txtdirect {
  enable www
}
```

Enable multiple types:

```
txtdirect {
  enable host path gometa dockerv2
}
```

Disable a specific type:

```
txtdirect {
  disable www
}
```

# DNS Resolver

---

To use a custom DNS resolver instead of the machine's default resolver, you can provide the `resolver` address in the config.

```
txtdirect {
  resolver 127.0.0.1:5353
}
```

# Logs

---

You can either use a file path or outputs like `stdout` and `stderr` as TXTDirect's logs output.
To configure a custom log output you can use the `logfile` field in the config:

```
txtdirect {
  logfile /path/to/file
}
```

Supported values are `stdout`, `stderr` or a file path. If empty, logs will get
discarded and written to `/dev/null`.
