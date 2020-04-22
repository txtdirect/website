+++
fragment = "table"
date = "2020-01-23"
weight = 100
background = "secondary"

title = "Prometheus Metrics"
subtitle= "List of metrics and their required labels"

[header]
  [[header.values]]
    text = "Metric Name"

  [[header.values]]
    text = "[Metric Labels](#metrics-labels)"
  
  [[header.values]]
    text = "Metric Description"

[[rows]]
  [[rows.values]]
    text = "txtdirect_redirect_count_total"

  [[rows.values]]
    text = "{host}"

  [[rows.values]]
    text = "Total requests per host"

[[rows]]
  [[rows.values]]
    text = "txtdirect_redirect_status_count_total"

  [[rows.values]]
    text = "{host, status}"

  [[rows.values]]
    text = "Total returned statuses per host"

[[rows]]
  [[rows.values]]
    text = "txtdirect_redirect_type_count_total"

  [[rows.values]]
    text = "{host, type}"

  [[rows.values]]
    text = "Total requests for each host based on type"

[[rows]]
  [[rows.values]]
    text = "txtdirect_fallback_type_count_total	"

  [[rows.values]]
    text = "{host, type, fallback}"

  [[rows.values]]
    text = "Total fallbacks triggered for each type"

[[rows]]
  [[rows.values]]
    text = "txtdirect_redirect_path_count_total	"

  [[rows.values]]
    text = "{host, path}"

  [[rows.values]]
    text = "Total redirects per path for each host"

+++
