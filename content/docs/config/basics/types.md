+++
fragment = "table"
date = "2020-01-23"
weight = 100
background = "secondary"

title = "Redirect Types"
subtitle= "List of supported redirect types"

[header]
  [[header.values]]
  text = "Type Name"

  [[header.values]]
  text = "Type Description"

[[rows]]
  [[rows.values]]
  text = "www"

  [[rows.values]]
  text = "Redirect all requests to \"www\"-subdomain"

[[rows]]
  [[rows.values]]
  text = "host"

  [[rows.values]]
  text = "Redirect to host provided in TXT record"

[[rows]]
  [[rows.values]]
  text = "path"

  [[rows.values]]
  text = "Enable path based redirects"

[[rows]]
  [[rows.values]]
  text = "gometa"

  [[rows.values]]
  text = "Enable Go package meta/vanity redirects"

[[rows]]
  [[rows.values]]
  text = "dockerv2"

  [[rows.values]]
  text = "Redirect to docker registry or image provided in TXT record"

[[rows]]
  [[rows.values]]
  text = "proxy"

  [[rows.values]]
  text = "Proxy the request to endpoint provided in TXT record"
+++
