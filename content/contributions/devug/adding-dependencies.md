# Chapter 2: Adding dependencies

When writing our `mypymodule` python module, we decided to use some other open source modules to
help out, specifically we decided to use the popular `numpy` and `scipy` modules.  We need to
tell the platform that these modules are required by anyone who wants to use `mypymodule`.  If
we have been preparing our module for installation with pip and have a `requirements.txt`, a
`pipfile` or a `pyproject.toml`, we can request that the state tool scan our project and add
these dependencies to our ingredient graphql file:
```
state ingredient scan /path/to/mypymodule/source
```
or if we're hosting our source on, e.g. Github, we could type:
```
state ingredient scan https://github.com/AwesomeProjects/mypymodule.git
```

These are convenient ways to add dependency information to our ingredient, and create a
`dependecy_sets` section in our ingredient file.  We can also create these manually.

## Manual dependency declaration

```graphql
       dependency_sets: [
         dependencies: [
           {
             conditions:                                # conditions required for this 
                                                        #   dependency to apply, usually null

             feature:                                   # name of the feature we depend on, 
                                                        #   e.g. another ingredient, build 
                                                        #   tool etc.

             namespace:                                 # namespace of the feature, e.g. 
                                                        #   'language', 'image'
             requirements: {
               comparator:                              # how we should compare versions, 
                                                        #   e.g. 'gte', 'eq', 'lte'

               version:                                 # the version of the feature we require
             }
           }
         ]
         description:                                   # description of the dependency
         type:                                          # type of this dependency, e.g. 'build',
                                                        #   'runtime', 'test'
       ]
```
