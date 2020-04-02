---
title: ActiveState Platform Changelog
draft: false
outputs:
    - HTML
    - JSON
---

## What's new

**February - March 2020**

### Enhancement: Python package catalog expanded to include the packages you need

* We've added a large set of around 20,000 Python packages/versions. The ActiveState Platform now have coverage of the important packages/versions in the Python ecosystem, and they're available for you to add to your projects.

### New Feature: State tool now supports requirements.txt

When you add packages to a Python project using the State Tool, you now have the option to specify the package requirements for the project in a `requirements.txt` file using the new `state packages import` command. For details, see the [packages Command](/state/packages.html) reference and [Creating projects from requirements.txt files](/projects/requirements-txt.html) for more general information on this feature.

### New Feature: Uploading requirements.txt now supported

When you create or update a Python project on the platform, you now have the option to provide the package and version requirements for the project in `requirements.txt` file format. You can copy and paste the contents of an existing requirements text file, or type in your project's requirements. 

![requirements.txt](../images/requirements-txt.png "requirements.txt support")

### New Feature: macOS now supported for custom runtimes

When you create a new custom project, or update an existing one, you can now specify macOS as a platform to build your language runtime for. When your build completes, you can download your custom runtime as a standard package installer.

![macOS support](../images/macos-runtime-support.png "macOS runtime support")

**NOTE**: Support for working with macOS projects with the State Tool is not yet supported. This feature is comming soon for the State Tool.

### New Feature: State Tool integration with popular CI/CD platforms

The State Tool is compatible with several popular continuous integration/continuous deployment tools to enable the setup of more secure, consistent, and up-to-date CI/CD pipelines.

The compatible CI/CD platforms are:

* Jenkins - See the [documentation](/state/jenkins.html).
* Travis CI - See the [blog post](https://www.activestate.com/blog/how-to-build-a-ci-cd-pipeline-for-python/) and [documentation](/state/travis.html).
* AppVeyor - See the [blog post](https://www.activestate.com/blog/how-to-simplify-ci-cd-pipelines-for-windows/) and [documentation](/state/appveyor.html).
* Github Actions - See the [blog post](https://www.activestate.com/blog/optimizing-ci-cd-pipelines-in-github-actions/)

### Komodo 12.0.1 

A maintenance release for Komodo 12 that resolves issues with State Tool integration identified in version 12.0, including a fix for login issues encountered due to State Tool failures. For the complete list of fixes, see <a href="http://docs.activestate.com/komodo/12/get/relnotes/" target="\_blank">Komodo 12 release notes</a>.

## Previous changes

**January 2020**

### New Feature: State Tool adds `package` command

The State Tool, the command line utility for the ActiveState Platform, includes a new `package` command you can use to manage packages in your projects. You can view, add, remove, and change the packages included in your project, and update your project on the Platform.

For more information about the `package` command, see the [command reference](/state/packages.html)

### Enhancement: Python catalog exceeds 20,000 packages/versions

You can now choose from over 20,000 unique packages/versions to add to your custom Python 2 and Python 3 projects.

### Enhancement: Request specific dependency versions

You now have selective control over the versions of dependencies that are included in your project. For example, if you include pandas in your project, numpy will be included as a dependency with a specific version.  You can now independently change the version of numpy to use.

![Request dependency](../images/request-specific-version.png)

### Enhancement: Commit messages

You can now optionally add commit messages to record your changes to a project with each commit.

![Commit message](../images/commit-message.png)

### New Feature: Komodo 12 available and integrated with the Platform

Komodo 12, the new release of ActiveState's Komodo IDE, includes the State Tool which enables seamless integration with the ActiveState Platform. 

Key features:

* Associate your new or existing Komodo project with an ActiveState Platform project. The Komodo project manages your source code, while the Platform project manages the core language distribution (e.g. Python 3.6.6) and the specific packages you have chosen to use with the runtime (e.g. Requests 2.18.4).
* Run State Tool commands from within Komodo using the toolbar or Commando. You can access the variety of commands the State Tool supports for viewing and working with Platform projects without leaving your editor.
* Work in the isolated "activated" environment created by the State Tool. When a project is activated, the State Tool downloads the language runtime, the packages you have selected and any dependencies, and sets up the activated virtual environment. When you run your code in Komodo you are using the ActiveState project language runtime isolated from any other runtimes you may have installed on your computer.

For more detailed information on these new features, see the State Tool integration section in the [Komodo 12 documentation](http://docs.activestate.com/komodo/12/state-integration/).

**December 2019**

### New Feature: ActiveTcl added

You can now create and build custom runtimes for Tcl 8.6.9 for Linux and Windows.

### Enhancement: ActivePython 2.7 updated to version 2.7.17

Python version 2.7.17, the penultimate release of Python 2, is now available on the Platform for creating custom builds. A Featured Project (Community Edition) for Python 2.7.17 will be available soon. 

### Enhancement: ActivePython 2 now supports a win32 option

When you add the Windows operating system to your build you have the option of selecting the 32-bit version for your operating system release. This is included for backwards compatibilty with older desktop computers and servers.

### Enhancement: New Python 2 and Python 3 packages now available

We've expanded our catalog of Python packages that you can use in your custom projects. The Platform currently supports over 3500 packages and we're adding more each week.

**November 2019**

### New Feature: GitHub authorization option added

You now have the option to use your GitHub credentials to create your ActiveState Platform account and authenticate with the Platform when you log in. When you authorize the ActiveState Platform to use your GitHub account for authentication, GitHub provides your email address, which ActiveState uses it to create your unique user account and link it with GitHub.

![GitHub authorization](../images/github-auth.png)

Note: Signing up for GitHub authentication requires that your email address and username are unique on the Platform. If you previously signed up for the Platform with the email you have associated with your GitHub account, or your GitHub username is already in use on the Platform, you cannot successfuly set up GitHub authentication at this time.  

**October 2019**

### Enhancement: Organization Members list now searchable

You can search for users in the **Members** tab by entering a full or partial username or email address. This helps you avoid scrolling through a long list of users to find the user or users you are looking for.

![Search the members tab](../images/member-search.png)

**September 2019**

### Enhancement: Project History now includes commit changes

The Project History now lists the packages, languages, and platforms that were added, updated, or removed in each commit allowing you to view the full history for the project's last 10 commits.

![Enhanced Project history](../images/project-history.png)

### Enhancement: Search added to Projects tab

You can now enter a partial name for a project in the new search text box to filter the projects listed in the projects tab. This allows you to quickly find the project you are interested in if you have a long list of projects.

![Enhanced Project search](../images/project-search.png)


### Enhancement: Builds tab displays platform specific links

You can now link directly to a specific platform on the Builds tab, which makes it easier to share builds with other users. For example, you can link directly to the Windows 10 build for a project. Previously you were only able to link to the default platform on Builds tab. To share a link to a particular platform, switch to the desired platform and copy the URL from your browser address bar.

![Enhanced Build tab links](../images/builds-platform-id.png)

**August 2019**

### Enhancement: ActivePerl and ActivePython Community Editions projects are now editable

You can now add or remove packages from ActivePerl 5.26 and 5.28, and ActivePython 3.6, on both Windows and Linux. This allows you to tailor our language distributions to your exact requirements. You can pick the packages and versions you need from our extensive catalog and create your own unique build. 

### Enhancement: State tool now integrates with CI/CD tools

The State Tool now runs without any interactive prompts, enabling you to install and configure it in Continuous Integration/Continuous Deployment workflows. For more information, see the State Tool [documentation](/state/ci.html). 

**July 2019**

### Enhancement: Streamlined form for creating projects

The form for creating new projects has been streamlined and simplified so you can quickly select the operating systems and language to include in your project, and choose if your project is public or private.

**Note**: Private projects are only available for paid accounts.

![New project](../images/projects-new.png)

![New project form](../images/projects-new-form.png)

### Enhancement: More help options for failed builds

If your build fails, you have a few options for moving forward:

- You can edit your project and try building it again.
- You can contact ActiveState for help with troubleshooting your build failure.
- You can download the ActiveState-managed project, or featured project, that is most similar to the build you are creating. 

The failed build page now provides more information and links for these options.

![Failed build options](../images/failed-build-options.png)

### New Feature: Success/Failure Build Notification Emails

You no longer need to keep checking on the status of your build. We'll let you know when it's done. The Platform now notifies you by email when a build finishes indicating whether the build succeeded or failed. If the build succeeded, you can click on a link in the email to return to the project page to download your build.

![Build Notification Email - Success!](../images/success-notifications.png)

### Release: State Tool update: Secrets, Scripts, Events, and more

A new release of the State Tool is available which includes a number of exciting new features for integrating the State Tool and Platform builds with your development environment.

The addition of constants and secrets allows you to manage configuration settings and other information for your project in the `activestate.yaml` configuration file. Secrets provide a simple and secure way to store and optionally share sensitive information, such as API keys and passwords.
Learn more about Secrets in this <a href="https://www.activestate.com/blog/developers-can-share-secrets-quickly-and-easily-without-sacrificing-security/" target="\_blank">blog post</a>.

Scripts and events provide ways to run additional logic required to configure your development environment. For example, you could configure an event to start your database server each time you activate your project. Scripts are run manually; events run when you ``state activate` your project.

**June 2019**

### New Feature: Custom Windows builds for ActivePerl and ActivePython

- You can now create you own customized ActivePerl and ActivePython distributions on Windows from scratch, or you can fork an existing project and customize it for you specific needs. After you build your project you can download the Windows installer (.msi) for your project, or use the State Tool to install it in a virtual environment.

    Note: Builds that are Managed by ActiveState cannot be customized. They are maintained by ActiveState, and if you fork these projects you regularly get the updated packages and dependencies as they are available. 

### Release: State Tool Preview

- A preview release of the State Tool is now available on Windows and Linux. The State Tool is the command line tool for the ActiveState Platform. Create a custom build or fork an ActiveState build, and then use the State Tool to download it and activate your project in a virtual environment. For details on getting started, see the [State Tool documentation](/state/).

    ![State Tool on Windows](../images/state-tool-windows.png)

### New Feature: Private Projects

- Paid users can create private projects. Users on the Coder, Team, Business, and Enterprise tiers can now create private projects. Private projects are restricted to members of the organization the project belongs to. Users on the Coder tier can create private projects that are only visible to themselves in their personal org. By default new projects on all tiers are public projects, which are visible to all users on the Platform.

    ![Private projects](../images/private-projects.png)

### New Feature: ActiveTcl Community Editions added to the Platform

- New language added! You can now download ActiveTcl builds from the **Featured Projects** page.
    
    ![ActiveTcl Projects](../images/activetcl-projects.png)

**May 2019**

- Improved **Build Status** information: You can now monitor the progress of your build including the total elapsed time, the success or failure of individual packages included in your build, and how long each package took to build. 

    ![Build status](../images/build-status.png)
    <br><br>
    ![Build success](../images/build-success.png)

- New top-level navigation menu for quickly accessing **Your Dashboard**, **Featured Projects**, and **Dev Tools** from anywhere in the Platform.<br> 

    ![Top-level navigation](../images/top-level-navbar.png)

- Red Hat Enterprise Linux 7 support: The Platform now supports builds with the latest Glibc version supported on RHEL 7 (glibc 2.17) and the latest kernel. Glibc is the main C library used by the Linux operating system, and the 2.17 release includes enhancements an bug fixes summarized <a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.0_release_notes/sect-red_hat_enterprise_linux-7.0_release_notes-compiler_and_tools-glibc" target="\_blank">here</a>. 
- New **Featured Projects** tab: Provides access to the latest ActivePython and ActivePerl managed projects -- projects that are curated and maintained by ActiveState. Currently available for Linux, these projects are the latest evolution of ActiveState Community Edition language distributions. You can view these projects to see the packages they contain, or fork them to make them accessible in your personal projects, or the projects that belong to any of the organizations you belong to. 

    ![Featured projects](../images/featured-projects.png)

- New **Dev Tools** tab: Access the latest edition of the Komodo IDE. For a limited time it's available to all Platform users. You can also try out the preview release of the State Tool, which enables you to work with your Platform projects in an isolated virtual environment. 

    ![Dev Tools](../images/dev-tools.png)

- Your **Dashboard** tab: Provides quick access to your personal homepage on the Platform.
- Delete projects: Added the ability to delete a project in the project **Settings** tab. 

**April 2019**

- You can rename your projects in the project **Settings** tab.
- You can create your own customized ActivePerl distributions on Linux.

    ![Customized ActivePerl project](../images/perl_custom_project.png) <br><br>

    ![Download customized build](../images/perl_download.png) 

- For ActivePerl projects, you can search by either package name or module name. For example, you can search for `mysql` and locate packages that include this search term in their name, or you can enter the `DateTime::Format::MySQL` to locate the exact package you need based on the module name.

    ![Perl package search](../images/package_search.png)

- You're sent directly to the **Build** tab your new project when you create a copy of a project, or a fork, from the ActiveState.com downloads page.
- Installer files are clearly differentiated from other files you can download from the **Project** > **Builds** tab. 

**March 2019**

- Fork Community Editions of <a href="https://platform.activestate.com/ActiveState/ActivePython-3.6.6/auto-fork" target="\_blank">ActivePython 3.6.6</a> and  <a href="https://platform.activestate.com/ActiveState/ActivePerl-5.26.3-CE/auto-fork" target="\_blank">ActivePerl 5.26.3</a> directly from the activestate.com downloads page.

- First release of the `state` tool, a command line interface for interacting with the ActiveState Platform and setting up projects in a local virtual environment.
- Copying, or forking, projects supported. For all projects, forking a project enables you to track updates to the project. For example, when ActiveState updates a managed project, such as ActivePerl-5.24, the changes including bug fixes and updated packages will be automatically available in your forked project. Currently, you can fork and modify two ActiveState Community Edition projects and add or remove packages, and then create your own custom distributions. This is a beta feature available now for ActivePython 3.6.6 and ActivePerl 5.26.3 on Linux.
- All users are now able to create and build projects.
- Recommended languages and platforms for creating builds are highlighted. Builds of projects created for Python 3.6.6 on Linux are the most likely to succeed.
- Build catalog increased to over 400 Python packages.

**February 2019**

- ActivePython 3.7.0 and 3.7.1 custom builds supported.
- Build catalog increased to over 300 Python packages available for selection.
- Dashboard **Latest Activity** now shows the 20 most recent activities.

**January 2019**

- Improved experience of creating a build by simplifying some of the language & platform options as well as guiding the user through the flow of getting to their first build.
- Our beta functionality of being able to make your own language builds are available for Python 2.7, 3.5 and 3.6 on Linux 64 (RHEL, CentOS, Ubuntu, Debian, and most other flavors using Glibc 2.12).

