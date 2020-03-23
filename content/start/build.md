---
title: "Custom language runtimes"
weight: 4
---

You can build a custom language runtime with the language, packages, and platforms you need.<!--more-->

**Important**: Customizing language builds is a work-in-progress feature. We're working hard on adding packages and optimizing the build experience. We recommend that you start with a small number of packages on your preferred operating system. Once your project builds successfully, you can experiment with additional options.

1. Open your web browser and navigate to <a href ="https://platform.activestate.com" target="\_blank">http://platform.activestate.com</a> and sign in.
2. To create a project for your personal use, click the **Projects** tab on your dashboard page.
3. To create a project in an Organization, select the Organization in the **Your Organizations** list and then click the **Projects** tab.
4. Click **Build a Custom Runtime**.
5. Enter a meaningful name for the project in **Project Name**. 
6. Projects are public by default. If you belong to an organization on a paid tier, you have the option of selecting **Private** to create a project that's only visible to members of the selected organization.
7. In **Choose a Language**, select the language to include and the version for each language.
8. In **Operating Systems**, select the operating system(s) where you will be installing the language distributions for your project. 
9. Click **Create Project**.

To add packages to your new project:

1. Click **Add Packages** to customize the packages included in your build. 
2. In the **Add Packages** dialog box, type in part of a package name and click **Search**. 
3. Click **Add** next to the package name to add a package from the search results. 
4. Repeat steps 2 and 3 to add additional packages, and click **Done** when you are finished adding packages.
5. Click **Commit Changes**. This is the step that starts the build in our server farm. The time it takes for the build to complete depends on the complexity of the build and the available resources to complete the build.
6. Click **View Status**. If the build status is In Progress, you can come back later to verify that the build completed successfully. In some cases, the build will fail immediately and you may need to adjust your settings and try again.
7. Once your build completes successfully, you can download the installer from the **Download Builds** tab or use the commands listed on the **Overview** page to activate your project using the [State Tool](/state/start). 