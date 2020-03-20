---
title: Creating custom projects
---

You can create custom projects that include only the ActiveState programming language distributions and packages you need for the specific operating systems you are working on. The Platform currently supports a wide variety of ActivePython and ActivePerl versions on Linux, Windows, and macOS.

1. Open your web browser and navigate to <a href ="https://platform.activestate.com" target="\_blank">http://platform.activestate.com</a> and sign in.
2. In the **Your Organizations** list, select the organization to create a custom build for, or click the **Projects** tab to create a personal project.
3. Click **Build a Custom Runtime**.
4. Enter a short, meaningful name for the project in **Project Name**.
5. In the **Select Languages** section, select the checkbox next to the language to include in the project, and then select the appropriate version from the drop-down list.

{{% notice tip %}}
To increase the likelihood of your build completing successfully, start with a recommended configuration, such as Python 3.6.6 on Linux or Windows, and add other languages once your project is building without errors.
{{% /notice %}}
    

6. In the **Select Platforms** section, click the platform operating system to use and then click the checkbox next to the platform(s) to include. The platforms list includes a description of the operating system versions the platform is for. 
7. Click **Create Project**.
8. Add packages to your project using the Customize your build options in the Requested packages panel:

    * Click **Choose Packages** to search for and add packages individually. 
    * Click **Import from requirements.txt** to add the set of packages and versions required for your project. For more information on specifying your project requirements using a `requirements.txt` file, see [Creating projects from requirements.txt files](/projects/requirements-txt).

    
    The packages you selected are listed in the **Requested Packages** list, and any dependencies of these selected packages are listed in the **Dependencies** list.

9. When you have reviewed the packages and dependencies that are included and you are satisfied, click **Commit Changes** to start the build process.
10. Click **View Status** to see the progress of the build. Depending on the packages included and the complexity of the build it can take quite a bit of time for the build to complete. You may need to come back later to access the finished build output. 
11. If the build completed successfully, you can download the installer for your build on the **Builds** page by clicking **Download**. For Linux, the file you want to download is named `ActivePython-linux-<platform>-<identifier>.tar.gz`. You do not need to download the recipe.json, packages, or tests files that are listed unless you specifically require them.

