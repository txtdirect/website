+++
fragment = "table"
date = "2020-01-23"
weight = 400
background = "secondary"

title = "txtd.io Subdomains"
subtitle= "List of subdomains for each type that you can use in `CNAME` and `A` records"

[header]
  [[header.values]]
  text = "URI"

  [[header.values]]
  text = "Description"

  [[header.values]]
  text = "Type Specification"

[[rows]]
  [[rows.values]]
  text = "txtd.io"

  [[rows.values]]
  text = "General - Used for `host` and `path` types"

  [[rows.values]]
  text = "[**host** - **path**](/docs/specification/)"

[[rows]]
  [[rows.values]]
  text = "docker.txtd.io"

  [[rows.values]]
  text = "dockerv2 - Redirect Docker CLI requests to a docker image or registry"

  [[rows.values]]
  text = "[**dockerv2**](/docs/specification/#dockerv2-type)"

[[rows]]
  [[rows.values]]
  text = "git.txtd.io"

  [[rows.values]]
  text = "git - Redirect requests to a git repository"

  [[rows.values]]
  text = "[**git**](/docs/specification/#git-type)"

[[rows]]
  [[rows.values]]
  text = "gometa.txtd.io"

  [[rows.values]]
  text = "gometa - Vanity URI for Go packages"

  [[rows.values]]
  text = "[**gometa**](/docs/specification/#gometa-type)"

[[rows]]
  [[rows.values]]
  text = "proxy.txtd.io"

  [[rows.values]]
  text = "proxy - Proxy requests to a custom upstream"

  [[rows.values]]
  text = "[**proxy**](/docs/specification/#proxy-type-experimental)"
+++
