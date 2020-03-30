---
title: "Mutations"
date: 2019-12-14T02:23:34Z
draft: true
---

```text
mutation Ingredient (
   name : "activestate/A"
   src : "data:,Hello%2C%20World!"
   builder : "activestate/builders/concat.sh@123"
   args: [ "hello.txt" ]
){
 id
 revision
 timestamp
}
```

## Response

```json
{
  "data" : {
    "id": "AAA-83838-03030-83838",
    "revision": 0,
    "timestamp": 1234
  }
}
```