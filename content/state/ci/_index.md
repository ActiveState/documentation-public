---
title: Using State Tool on CI/CD
aliases:
    - /state/ci.html
weight: 63
---

You can use the State Tool with your Continuous Integration/Continuous Delivery (CI/CD) processes and and tools. You can use the State Tool to define simple and reliable processes for building, testing, and deploying your software projects.

The State Tool can be silently installed for your CI/CD, download a custom language runtime with your code's specific language and package requirements, and run scripts as required throughout the build process.

The basic process you need to follow is:

1. Gather environment variable settings: Retrieve the environment variables required to authenticate with the ActiveState Platform and (optionally) use secrets in your CI/CD configuration file and build scripts.
2. CI/CD Setup: Configure the integration between your CI/CD and your code repository. For example, link your GitHub repository to your AppVeyor account and provide the necessary authorization to AppVeyor.
3. Platform Setup: Create a Platform project with your language, platform (operating system), and package requirements.
4. Configure `activestate.yml`: `state activate` to generate the `activestate.yml` file for the project and add it to your code repository.
5. Build Setup: Add a configuration file to your repository with the build configuration for your CI/CD tool that installs the State Tool and runs any other build steps. For example, a `Jenkinsfile` for Jenkins, or a `appveyor.yml` file for AppVeyor.
6. Webhook Setup: Add a webhook to your version control repository if required. In some cases this may be completed automatically when you are integrating your code repository with the CI/CD tool in step 2. In other cases, it may be a manual step you need to complete. 

* [Setup and configuration for Jenkins](jenkins.html)
* [Setup and configuration for AppVeyor](appveyor.html). Also check out the related [blog post](https://www.activestate.com/blog/how-to-simplify-ci-cd-pipelines-for-windows/)
* [Setup and configuration for Travis](travis.html). Also check out the related [blog post](https://www.activestate.com/blog/how-to-build-a-ci-cd-pipeline-for-python/)
* [Setup and configuration for GitHub Actions](github-actions.html). Also check out the related [blog post](https://www.activestate.com/blog/optimizing-ci-cd-pipelines-in-github-actions/)


