# Chapter 1: Adding your first ingredient

In order to add a new ingredient, it's easiest to use the state tool to create a template
ingredient file which you can add detail to.  We'll create an ingredient for a python module
called `mypymodule` which we'll suppose is ready for release. Run
```
state ingredient new mypymodule --version 0.0.1 --namespace language/python
```
This will create a `mypymodule` directory under your current working directory with a single
template file `mypymodule.graphql` in it.  The file will look like this:
```graphql
mutation Ingredient (
  name:              "mypymodule"                       # name of the ingredient
  primary_namespace: "language/python"                  # the namespace the ingredient should
                                                        #   belong to
  description:                                          # a short description of the ingredient
  website:                                              # the ingredient's website, if it has one
  versions: [
    {
       version:           "0.0.1"                       # the raw version of the ingredient
       is_stable_release: true                          # true if this release is stable, 
                                                        #   false otherwise

       release_timestamp: "1970-01-01T00:00:00.000000Z" # date/time of release

       source_uri:                                      # URI to the source code as a zip 

       build_rule: {
         platform: []                                   # a list of platform features required 
                                                        #   for this toolchain to be selected

         toolchain: python-builder                      # URI to a toolchain implementation
       }
       provided_features: [
         feature: "mypymodule"                          # name of the feature this version 
                                                        #   provides, usually the ingredient
                                                        #   name

         version: "0.0.1"                               # version of the feature provided
         is_default_provider: true                      # false if this is an alternative 
                                                        #   provider for a feature

         namespace: "language/python"                   # namespace of the feature, usually 
                                                        #   the same as the namespace of the 
                                                        #   ingredient
       ]
     }
  ]
){
  id
  revision
  timestamp
}
```

This represents the minimum level of information required by the ActiveState Platform to
incorporate and build this module and much of it has been pre-filled.  It takes the form of a
graphql mutation which gives us a great deal of flexibility in what information we want to
submit to the platform about our ingredient.  Go ahead and open this file in your favourite
editor and we'll tackle the data section-by-section.

## General info

```graphql
  name:              "mypymodule"                       # name of the ingredient
  primary_namespace: "language/python"                  # the namespace the ingredient should
                                                        #   belong to
  description:                                          # a short description of the ingredient
  website:                                              # the ingredient's website, if it has one
```

These represent some basic information about the ingredient; `name` is autofilled by the state
tool based on the arguments to `state ingredient new`, as is `primary_namespace`.  The platform
has a range of namespaces, described further in the [Namespaces](namespaces.md) document but for
now, all we need to know is that `language/python` is the correct choice for a python module.
The `descripton` field is a short (a few words) description of the module and the `website`
should be the URL of the module's home page.  This latter field is optional, but included here
because most projects will have one, even if it is a just a hosted git repo.

Let's fill those in:
```graphql
  description: "The most awesome Python module"
  website: "https://example.org/mypymodule"
```
## Versions
```graphql
  versions: [
```
The platform supports uploading data about multiple versions in one submission, but we're
only adding a single version so we can use a single object array.
```graphql
    {
       version:           "0.0.1"                       # the raw version of the ingredient
       is_stable_release: true                          # true if this release is stable, 
                                                        #   false otherwise

       release_timestamp: "1970-01-01T00:00:00.000000Z" # date/time of release
       source_uri:                                      # URI to the source code as a zip 
```
The state tool has added the `version` string we specified in the arguments to `state
ingredient new`.  It's added here rather than at the top level as, as explained above, we are
able to submit multiple versions at once should we so wish.  The `is_stable_release` flag is to
indicate whether or not this is a stable release as opposed to a beta or release candidate.  The
platform also requires the `release_timestamp` for the version, which indicates when this
version was released to the world as opposed to the date it was added to the platform.  The
default timestamp shown here is for illustration purposes only, to show the required format
(__TODO: other formats may be usable here too?__).  Finally, the `source_uri` field tells the
platform where it can download the source code for this version from as a tarball or zip file.

Let's fill in the missing information:
```graphql
       release_timestamp: "2019-09-15T12:00:00.000000Z"
       source_uri: "https://example.org/mypymodule/download/mypymodule-0.0.1.tar.gz"
```
## Build information
```graphql
       build_rule: {
         platform: []                                   # a list of platform features required 
                                                        #   for this toolchain to be selected

         toolchain: python-builder                      # URI to a toolchain implementation
       }
```
The `build_rule` section is where we tell the platform how to build our module.  In this case,
our module is designed to be built and installed with python's `setuptools` so we can safely use
the `python-builder` toolchain on all platforms.  We don't need to specify any
platform constraints (e.g. operating system, cpu architecture) for this, although we could
specify different toolchains to use on e.g. linux and windows should we need to.  Toolchains are
discussed further in the [Toolchains](toolchains.md) document.
## Feature provision
```graphql
       provided_features: [
         feature: "mypymodule"                          # name of the feature this version 
                                                        #   provides, usually the ingredient
                                                        #   name

         version: "0.0.1"                               # version of the feature provided
         is_default_provider: true                      # false if this is an alternative 
                                                        #   provider for a feature

         namespace: "language/python"                   # namespace of the feature, usually 
                                                        #   the same as the namespace of the 
                                                        #   ingredient
       ]
```
This section tells the platform about the features that this module provides.  The platform
supports the notion of several ingredients being able to provide the same feature so that
alternative providers are available should project maintainers want to give users a choice when
dependencies are being resolved.  This gives users, for example, the option to choose from 2
API-compatible libraries to provide implementations of that API as in the case of OpenSSL and
LibreSSL.  Here, we are the only provider of our module's API so we will fill in the details of
our module, essentially declaring that we are providing `mypymodule`'s API and/or other feature
set and declaring that our module should be the default provider for anything that requires
`mypymodule` via the `is_default_provider` field.  Features are discussed in more detail in the
[Features](features.md) document.
```graphql
){
  id
  revision
  timestamp
}
```
This last section is what we would like to be told about our newly created ingredient once it is
created: the system-assigned `id`, the `revision` of the ingredient we created (discussed
further in [Revisions](revisions.md)) and the platform `timestamp` of when the ingredient was
added to the platform.

Now we've filled in the blank portions, we can submit this new ingredient to the platform using
`state ingredient add mypymodule.graphql`

## TODO: discussion of error conditions and how to correct them
