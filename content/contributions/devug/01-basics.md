---
title: First principals
---
##  Ingredient **A** whose source is the content "Hello World!"

It uses the concat builder and sends the hello.txt argument

**Request**

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

**Response**

```json
{
  "data" : {
    "id": "AAA-83838-03030-83838",
    "revision": 0,
    "timestamp": 1234
  }
}
```


## A builder is just a shell script in a git repo

Note the concat builder takes a url and saves it's results to the name that was set as the first argument.

It's implementated in the `ActiveState/builders` git repo

```bash
  builders/
    concat.sh
```

It's contents are simply (note being hand wavy on how you get a data url to contents is bash...)

```bash
echo data_url_to_file($SRC) > $out/$1
```


## We can retreive the artifacts for the ingredient if it were built at time 1234

The `artifacts()` query will return a list of artifact records that include it's status, version and revisions.
Each artifact will have a list of URLs that are the output results after the build process.


**Request**

```text
query {
  timestamp
  artifacts(attime=1234, platform=macos requirments=["activestate/A"]){
     name
     status
     revision
     urls
  }
}
```

**Response**

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

## Defining an ingredient with a dependency

There is an ingredient B who depends on A

**Request**

 ```text
mutation Ingredient (
 name : "activestate/B"
 src : "http://activestate.com/some-other-file"
 builder: activestate/builders/zip.py@123
 requires [
    Any("activestate/A/hello.txt") ; Requires Any activestate/A that has a hello.txt
 ]
){
  timestamp
  id
  revision
}
``` 

**Response**

```json
{
  "data" : {
    "timestamp": 1235,
    "id": "BBB-83838-03030-83838",
    "revision": 0
  }
}
```

Above we created an ingredient **B** who depends on A and uses `some-other-builder.py` to build it whose contents look like this:

```python
from zipfile import ZipFile
import os
import json

SRC = os.environ['SRC']
OUT = os.environ['OUT']
REQUIREMENTS = json.loads(os.environ['REQUIREMENTS'])

OUT_PATH = os.path.join(OUT, os.path.basename(SRC), '.zip')

with ZipFile(OUT_PATH, 'w') as myzip:
    myzip.write(SRC)
    myzip.write(REQUIRMENTS['activestate/A/hello.txt'])
```

Note this time we used a builder script written in python which creates a new zipfile named after our SRC (in this case `some-other-file.zip`). In the zip is placed the SRC which is `http://activestate.com/some-other-file` *AND* `hello.txt` which was available from activestate/A.

Requirements are passed as a JSON structure, the contents and other metadata is available in the REQUIREMENTS json structure. The zip builder uses this information to locate the contents of `hello.txt` and include it in the `some-other-file.zip`

**Request**

```text
query {
  timestamp
  artifacts(attime=1234, platform=macos requirments=["activestate/B"]){
     name
     status
     revision
     urls
  }
}
```

**Response**

```json
{
  "errors" : {
    "message": "There are no ingredients that sastisfy the requirement activestate/B at or before timestamp 1234"

  }
}
```

Ack! What happened! Note every addition to the graph is kept for all time. We added `activestate/B` some time after 1234. In order to maintain reproducability, certain queries like `archive()` require a `attime:Timestmap` to determine which changes it will consider when making the build. Because we specified a timestamp prior to the addition of `activestate/B` the system is telling us it does not exist. Let's try again with an updated timestamp.

**Request**

```text
query {
  timestamp
  artifacts(attime=2007, platform=macos requirments=["activestate/A"]){
     name
     status
     revision
     urls
  }
}
```

**Response**

```json
{
  "data" : {
    "timestamp": 1235,
    "artifacts" : [{
       "name" :"activestate/B", 
        "status": "BUILT",
        "revision": 0,
        "version": 0,
        "urls": ["http://activestate.com/storage/BBB-83838-03030-83838-activestate-B/some-other-file.zip"]
      }
    ]
  }
}
```

Because we asked for `activestate/B` we only received the artifacts for B. There's nothing stopping us from asking for both the artifacts of `A` *and* `B`

```text
query {
  timestamp
  artifacts(
    attime=2007, 
    platform=macos, 
    requirments=[
       "activestate/A"
        "activestate/B"
    ]
   ){
     name
     status
     revision
     urls
  }
}
```

**Response**

```json
{
  "data" : {
    "timestamp": 1235,
    "artifacts" : [{
       "name" :"activestate/A",
        "status": "BUILT",
        "revision": 0,
        "version": 0,
        "urls": ["http://activestate.com/storage/AAA-83838-03030-83838-activestate-A/hello.txt"]
      },
      {
       "name" :"activestate/B",
        "status": "BUILT",
        "revision": 0,
        "version": 0,
        "urls": ["http://activestate.com/storage/BBB-83838-03030-83838-activestate-B/some-other-file.zip"]
      }
    ]
  }
}
```

## Updating an Ingredient

You update an ingredient the same way you add them

**Request**

 ```text
mutation Ingredient (
 name : "activestate/A"
 src : "data:,Hi%2C%20Mom!"
 builder : activestate/builders/concat.sh@123
 args: [ "hello.txt" ]
){
  id
  revision
  timestamp
}
``` 

**Response**

```json
{
  "data" : {
    "id": "CCC-8929038-0030-83838",
    "revision": 1,
    "timestamp": 2009
  }
}
```

We changed the source URL which produces a new revision of the Ingredient we added previously in addition the id was updated. If we ask for the artifacts of A now with a newer timestamp.

**Request**

```text
query {
  timestamp
  artifacts(attime=2009, platform=macos requirments=["activestate/A"]){
     name
     status
     revision
     urls
  }
}
```


**Response**

```json
{
  "data" : {
    "timestamp": 2009,
    "artifacts" : [{
        "name": "activestate/A",
        "status": "BUILT",
        "revision": 1,
        "urls": ["http://activestate.com/storage/CBIC-1234-838-8323-activestate-A/hello.txt"]
      }
    ]
  }
}
```

We receive an artifact whith a different content addresable hash

In fact, because 'B' depends on 'A' it to will have a different artifact (assuming you use the later timestamp).

**Request**

```text
query {
  timestamp
  artifacts(attime=2009, platform=macos requirments=["activestate/B"]){
     name
     status
     revision
     urls
  }
}
```

**Response**

```json
{
  "data" : {
    "timestamp": 2009,
    "artifacts" : [{
        "name": "activestate/B",
        "status": "BUILT",
        "revision": 0,
        "urls": ["http://activestate.com/storage/ZIRE-20937-0ee0-83838-activestate-B/some-other-file.zip"]
      }
    ]
  }
}
```

What if we made a huge mistake and want to revert?

**Request**

 ```text
mutation Ingredient (
 name : "activestate/A"
 src : "data:,Hello%2C%20World!"
 builder : activestate/builders/concat.sh@123
 args: [ "hello.txt" ]
){
  id
  revision
  timestamp
}
``` 

**Response**

```json
{
  "data" : {
    "id": "AAA-83838-03030-83838",
    "revision": 3,
    "timestamp": 2012
  }
}
```

**NOTE: wonder why we even bother with a revision number **

As before the revision number incremented. But something curious happens when asking for the artifacts.

**Request**

```text
query {
  timestamp
  artifacts(attime=2012, platform=macos requirments=["activestate/A"]){
     name
     status
     revision
     urls
  }
}
```

**Response**

```json
{
  "data" : {
    "timestamp": 2012,
    "artifacts" : [{
        "name": "activestate/A",
        "status": "BUILT",
        "revision": 3,
        "version": 0,
        "urls": ["http://activestate.com/storage/AAA-83838-03030-83838-activestate-A/hello.txt"]
      }
    ]
  }
}
```

You'll note that the URL is the same for revision 0 of `activestate/A`. That's because the system detected we're using the same inputs and the same builder therefore determined it could safely reuse the old output.
