---
title: "Queries"
date: 2019-12-14T02:24:16Z
draft: true
---

```text
{
  timestamp
  artifacts(attime=1234, platform=macos requirements=["activestate/A"])
  {
     name
     status
     revision
     urls
  }
}
```

## Response

```json
{
  "data" : {
    "timestamp": 1234,
    "artifacts" : [{
        "name": "activestate/A",
        "status": "BUILT",
        "revision": 0,
        "version": 0,
        "urls": ["http://activestate.com/storage/AAA-83838-03030-83838-activestate-A/hello.txt"]
     }]  
  }
}
```


You can query the schema to discover details about the API interactively.

[Run in GraphiQL](https://swapi.graph.cool/?query=%7B%0A%20%20__schema%7B%0A%20%20%20%20types%20%7B%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20kind%0A%20%20%20%20%20%20fields%7B%0A%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%20description%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D)

```text
{
  __schema{
    types {
      name
      kind
      fields{
        name
        description
      }
    }
  }
}
```


[Run in GraphiQL](https://swapi.graph.cool/?query=%7B%0A%20%20__type%28name%3A%22FilmPreviousValues%22%29%20%7B%0A%20%20%20%20name%0A%20%20%20%20kind%0A%20%20%20%20description%0A%20%20%20%20fields%7B%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20type%20%7B%0A%20%20%20%20%20%20%20%20kind%0A%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D)

```text
{
  __type(name:"FilmPreviousValues") {
    name
    kind
    description
    fields{
      name
      type {
        kind
        name
      }
    }
  }
}
```

