+++
fragment = "table"
date = "2020-01-23"
weight = 100
background = "secondary"

title = "Placeholders"
subtitle= "TXTDirect supports various placeholders. These can be used to create more dynamic redirects"

[header]
  [[header.values]]
    text = "Placeholder"

  [[header.values]]
    text = "Value"
  
[[rows]]
  [[rows.values]]
    text = "**{~cookie}**"

  [[rows.values]]
    text = "The value of a cookie, where \"cookie\" is the cookie name"

[[rows]]
  [[rows.values]]
    text = "**{dir}**"

  [[rows.values]]
    text = "The directory of the requested file (from request URI)"

[[rows]]
  [[rows.values]]
    text = "**{file}**"

  [[rows.values]]
    text = "The name of the requested file (from request URI)"

[[rows]]
  [[rows.values]]
    text = "**{fragment}**"

  [[rows.values]]
    text = "The last part of the URL starting with \"#\""

[[rows]]
  [[rows.values]]
    text = "**{>Header}**"

  [[rows.values]]
    text = "Any request header, where \"Header\" is the header field name"

[[rows]]
  [[rows.values]]
    text = "**{host}**"

  [[rows.values]]
    text = "The host value on the request"

[[rows]]
  [[rows.values]]
    text = "**{hostonly}**"

  [[rows.values]]
    text = "Same as {host} but without port information"

[[rows]]
  [[rows.values]]
    text = "**{labelN}**"

  [[rows.values]]
    text = "The Nth label of the host (where N is an integer, at least 1) such as {label1}.{label2}.{label3}."

[[rows]]
  [[rows.values]]
    text = "**{method}**"

  [[rows.values]]
    text = "The request method (GET, POST, etc.)"

[[rows]]
  [[rows.values]]
    text = "**{path}**"

  [[rows.values]]
    text = "The path portion of the original request URI (does not include query string or fragment)"

[[rows]]
  [[rows.values]]
    text = "**{path_escaped}**"

  [[rows.values]]
    text = "Query-escaped variant of {path}"

[[rows]]
  [[rows.values]]
    text = "**{port}**"

  [[rows.values]]
    text = "The client's port"

[[rows]]
  [[rows.values]]
    text = "**{query}**"

  [[rows.values]]
    text = "The query string portion of the URL, without leading \"?\""

[[rows]]
  [[rows.values]]
    text = "**{query_escaped}**"

  [[rows.values]]
    text = "The query-escaped variant of {query}"

[[rows]]
  [[rows.values]]
    text = "**{?key}**"

  [[rows.values]]
    text = "The value of the \"key\" argument from the query string"

[[rows]]
  [[rows.values]]
    text = "**{uri}**"

  [[rows.values]]
    text = "The request URI (includes path, query string, and fragment)"

[[rows]]
  [[rows.values]]
    text = "**{uri_escaped}**"

  [[rows.values]]
    text = "The query-escaped variant of {uri}"

[[rows]]
  [[rows.values]]
    text = "**{user}**"

  [[rows.values]]
    text = "The username authorized by basicauth (HTTP Basic Authentication)"

+++
