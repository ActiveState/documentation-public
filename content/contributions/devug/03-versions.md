---
title: Versions
---

In previous examples we showed you how to add simple ingredients to the BuildGraph 
without any kind of lineage. Every edit we posted was a Revision to the single
Ingredient. The revision you are given when asking for Artifacts depends entirely
on the time stamp given. Software authors however often ship source for multiple
versions of the same software. The BuildGraph models this as well and gives you
powerful tools to choose the most appropriate version for your requirments. 

When specified correctly, you can later Query the BuildGraph with new time stamps and
ask for Artifacts which will be rebuilt (or given cached copies) with updates so long as they satisfy all your constraints. 

To see this in action will continue from our examples in the previous chapter
but first introduce you to the `solve()` query.

## Asking for the build plan

You've seen the `artifacts()` query which will retrieve the results of building an ingredient. Another
query you should be aware of is the `solve()` query which uses the same arguments of `artifacts()`
to return a build plan (we call this a `Recipe`) of your ingredient along with all of it's Transitive Depedencies (Your ingredient's dependencies, your dependencies dependencies and so on). When you use the  `artifacts()` it internally uses the `solve()` command to determine everything that needs to be built in order to return the artifacts that you've requested. 

One interesting thing to understand about requirements, you are not actually specifying ingredients directly by name. Instead you are providing a series of constraints to the Solver whose job it is to find you the best Ingredients that match your requirements for a particular point in time. The solver will always return the exact same `Recipe` for the given timestamp and platform you specify. In order to get a different results you either need to change the constraints or new ingredient revisions need to be added and you must provide a newer timestamp to have them included in the
calculation.

A few examples will help build up your intuition.

### Adding a Versioned Ingredient

We need to add a Versioned Ingredient to the BuildGraph. 

```text
mutation Ingredient (
   name : "activestate/A"
   src : "data:,Bonjour%2C%20World!"
   builder : "activestate/builders/concat.sh@123"
   version: 1
   args: [ "hello.txt" ]
){
 id
 revision
 timestamp
}
```

Multiple Versions of an Ingredient can exist in BuildGraph at the same time. This differs

## Version Specifiers

Side note. It is important  to understand the BuildGraph is designed
to build Ingredients from many different Software Eco Systems. These Eco Systems
all have their own Versioning schemes. Some Eco Systems have very explicit rules
for the software release process and how versions are specified as strings. There
are standards like SemVer which specify versions as always having the form 
`<major>.<minor>.<patch> i.e. 1.2.3` while others schemas can be as 
ridiculous as `apples, bannans, oranges`.  Because, unfortunately, not all Eco Systems
are explicit about their Version Schemas and leave it to the Authors to do whatever
they want. And unfortunately they do.

Our goal with the graph is to let you find and work with Ingredients using the natural
version numbers you're familiar with. And so we've created a system to unify these
Versions Standards.

How we do this ... is to understand that Versioning at its essence is simply
a way of providing an ordering independent of time. We have created an internal
representation of this ordering and it's up to Ingredient Contributors to provide
paresers that can convert a Version for some Versioning Schema to an Ordering that
we understand. The platform today provides several Version Type specifiers and
every Ingredient must be assosciated with one. 

The platform provides several Version Schemas today:

* SemVer
* Perl
* AlphaSort

And there's a guide for extending these as needed.
