---
title: Packaging
---

We provide several Packagers that will take Artifacts out of the Build Graph and convert them to a format that
you can use natively. Packagers have an number of common required arguments and fields in common. These
describe the Artifacts that the packager needs.

## Common

```text
query {
   ; packager using atTime/requirements
   packager(atTime=1234, platform="II-X") {
      fields...
   }
   
   ; packager referencing an order
   packager(commitId = "AA7-IXX...") {
      fields...
   }
}
```

### Common arguments
In addition to packager specific arguments all packagers require one of more of the following attributes.


| Argument             | Descrption                                                                 |
|----------------------|----------------------------------------------------------------------------|
| **atTime**           | Mandatory, only changes to graph at or before this time will be considered |
| **requirements**     | List of requirements and constraints. Either  `requirements` can be specified or `orderId` but not both. |
| **order**            | A Url to an order which contains the timestamp and requirements. Either an order can be specified or you must use `requirements` and `atTime` but not both. |
| **platform**         | Id of a platform which represents an operating system, hardware architecture|

### Common Fields

| Field                | Descrption                                                                 |
|----------------------|----------------------------------------------------------------------------|
| **atTime**        | Timestamp needed to reproduce this package exactly |
| **requirements**     | List of requirements and constraints. Either  `requirements` can be specified or `orderId` but not both |
| **order**            | A Url to an order which contains the timestamp and requirements. Either an  order can be specified or you must use `requirements` and `atTime` but not both. |

## Artifacts

You've already been introduced to the fundamental packager query `artifacts` it can retrive the artifacts from one or more ingredients
start building them if they haven't been built otherwise returning the results.

```text
query {
   artifacts(atTime=1234, platform="II-X", requirment=["namespace/feature"]) {
      urls
   }
}
```

## Docker

Is a packager that will take an artifact from the Build Graph and package it's content into a docker image that can be deployed to a repository somewhere.

```text
query {
   docker(atTime=1234, platform="II-X", requirment=["namespace/feature"]) {
      urls
   }
}
```


## Legacy Installer

You've already been introduced to the fundamental packager query `artifacts` it can retrive the artifacts from one or more ingredients
start building them if they haven't been built otherwise returning the results.

```text
query {
   installer(atTime=1234, platform="II-X", requirment=["namespace/feature"]) {
      urls
   }
}
```

## Python Wheels

This will package all python requirments into a list of wheels. Note it is an error to specify requirements that are not Python. We'll have to figure out how to distinguish system libraries
from python packages. Will we do this by namespace? Or do we let you build anything and ship you the wheel we find? 

```text
query {
   wheels(atTime=1234, platform="II-X", requirement=["namespace/feature"]) {
      urls
   }
}
```

