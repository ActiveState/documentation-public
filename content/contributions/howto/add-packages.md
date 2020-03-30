---
title: "Add Packages"
date: 2019-12-14
---

## Step 1: Get your authentication token/API key and organization id

The Dashboard API service is responsible for authenticating a user and providing a token that will need to be included in all future API requests to this service and all other services the user needs to communicate with.

This service is also responsible for knowing which organizations a user belongs to. In order to create a private ingredient, the ingredient needs to be associated with an organization, specifically an organization ID. After logging in, the ID of the organization the ingredient will belong to can be retrieved from this service.

If you are adding a private ingredient you will also need to get the 

## Step 2: Check the list of available packages

You can query the Inventory API to verify that the package and version you wnat to contribute does not currently exist in our package repository.

## Step 3: Create a package definition

Define a GraphQL mutation with the information require to build the package. See the [Mutations](/reference/mutations/) section for examples.

## Step 4: Submit your package to builder

Submit the GraphQL query to add the new package entry and schedule a build. In the REST API this involves a number of calls:

* Submit the order to the /recipes endpoint
* Submit the recipe to the /builds endpoint
* Check /builds/{build_request_id} for status
* Once the build completes /builds will return an array of artifacts

For info on the new wrapper approach, see the [Wrapper Spec] document.(https://docs.google.com/document/d/1IEIloqyjckx_qKTQ-Hbo5-ilpNR53HsG_XRq8NjGvRo/edit)

## Step 5: View the results

Depending on the complexity of the package you are building and the number of platforms you are building it for, the build process may take some time. If the build is successful you will be notfied that the package has been added to the inventory and a list of artifact links will be returned. Otherwise the builder will present you with failure information including the specific errors encountered and the full build log. For the steps to take to resolve any issues that arise, see Troubleshooting build failures (#troubleshooting-build-failures).


## Troubleshooting build failures

* List things that they can fix and steps to take.
* Indicate issues they won't be able to solve, who to contact, what the expected resolution time is.