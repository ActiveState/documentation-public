# Extended toolchain descriptor for an ingredient
## Composable toolchains
**Note:** This document describes how an ingredient would describe the toolchain(s) required to build it, not how we would define a toolchain within the platform

This is a sample blank ingredient with an example of a possible extended toochain descriptor.  Note it has an `executor` toolchain which should be present on the build image and whose definition should contain the mechanism for running this kind of build.  It also has multiple `adjunct` toolchains which only need to be present on the build image.  Together with any platform restrictions listed here and the platform restrictions which come in via the order, these form a set of constraints for the build image.

All toolchain definitions should declare multiple platform variants, the variant to be chosen by the solver based on order constraints (e.g. `devtoolset-6` on `CentOS7` with cpu `x86_64` would resolve to a unique concrete instance of a toolchain)

We may want to allow multiple toolchains of the same type to be present in the same image (e.g. `devtoolset-6` and `devtoolset-7`) where this is possible.  In this case, the toolchain definitions should contain mechanisms for selecting themselves for the build (e.g. set `PATH`, use debian `alternatives`, run `vcvars.bat`)

The extended descriptor below has features to supply options to a toolchain in both generic (e.g. `env` vars) and toolchain-specific (e.g. `conf_args`) sections.  The sections applicable to a toolchain should be composed from a generic set and any defined by the toolchain itself.  It also supplies a mechanism (dubbed `translations` below) in which a toolchain descriptor may flesh out (or override) how certain build flags are expressed.  In this example, we state that a request for a debug build should be expressed as a new `configure` argument (`--enable-symbols`) and that a thread-enabled build should be expressed as both a `configure` argument (`--enable-threads`) and an additional environment variable (`LIBS=-lpthread`)
```
name: # the name of the ingredient
primary_namespace: # the namespace the ingredient should belong to
description: # a short description of the ingredient
website: # the ingredient's website, if it has one
versions:
- version: # the raw version of the ingredient
  authors: # a list of the authors, by name
  copyright_text: # the body of the license
  license_expression: Unknown
  release_timestamp: '1970-01-01T00:00:00.000000Z'
  documentation_uri: # URI of the documentation for this version, if known 
  is_binary_only: # false if the source code is available, true otherwise
  source_uri: # URI to the source code as a zip file or tarball
  build_rule:
    - platform: [] # a list of platform features required for this toolchain
      toolchain: 
      - executor:
        - autoconf: 1.2.3
          env:
            - var1: value1
            - var2: value2
          conf_args:
            - flag1: value1
            - flag2: value2
          translation: # need a better name for this.  expression? override?
            - debug:
              - conf_args:
                - enable-symbols:
            - threaded:
              - conf_args:
                - enable-threads:
              - env:
                - LIBS: -lpthread
      - adjunct:
        - devtoolset: 6
          X11-dev: 4
  is_stable_release: # true if this release is stable, false otherwise
  provided_features:
  - feature: # name of the feature this version provides, usually the ingredient name
    version: # version of the feature provided
    is_default_provider: # false if this is an alternative provider for a feature
    namespace: # namespace of the feature, usually the same as the namespace of the ingredient
  dependency_sets:
  - dependencies:
    - conditions: # conditions required for this dependency to apply, usually null
      feature: # name of the feature we depend on, e.g. another ingredient, build tool etc.
      namespace: # namespace of the feature, e.g. 'language', 'image'
      requirements:
      - comparator: # how we should compare versions, e.g. 'gte', 'eq', 'lte'
        version: # the version of the feature we require
    description: # description of the dependency
    original_requirement: null
    type: # type of this dependency, e.g. 'build', 'runtime', 'test'
```
