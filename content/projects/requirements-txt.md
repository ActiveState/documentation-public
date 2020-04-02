---
title: "Creating projects from requirements.txt files"
---

If you have an existing Python project that you want to add to the Platform, you can export a `requirements.txt` file to get a list of packages and versions to import into your Platform project, or you can type in the list of packages and versions manually.

## Generating requirements.txt files

To generate a requirements.txt file:

* You can write out the requirements for an existing project to a `requirements.txt` file using one of the following commands at your command prompt:

    ```text
    # python2
    python -m pip freeze > requirements.txt

    # python3
    python3 -m pip freeze > requirements.txt
    ```

## Creating new projects

To create a project from `requirements.txt`:

1. Navigate to your organization and create a new project by clicking **Build a Custom Runtime**. You must choose Python as the language.
2. Click **Import from requirements.txt**  in the **Requested Packages** panel.
3. Open the `requirements.txt` to use and copy and paste the content, or type in your requirements individually.

![requirements.txt](../../images/requirements-txt.png "requirements.txt entries for import")

4. Click **Import**.
    <br><br>The Platform parses each entry in your `requirements.txt` file and validates the syntax, and identifies any issues. When the file is valid, the platform attempts to match each package requirement with a package and version available on the platform. For supported syntax, see [requirements.txt syntax](#requirements-txt-syntax).
    
   ![Parsed packages](../../images/parsed-packages.png)

5. If any errors or mismatches are identified between the requirements you have defined in your `requirements.txt` file and the package and versions available on the Platform, you may be able to adjust the package versions individually to create a valid build request.
6. Click **Commit Changes**.
    In **Requested Packages** you will see each package listed, along with the requested version and the version selected by the Platform to fulfill the requirement.

7. Click **View Status** to start the build and view the build progress. It may take some time for the build to succeed or fail, but you will receive an email notification when the build finishes.
8. Once the build completes successfully, you have two options for accessing your build:
    1. You can download the installer(s) for your platform(s)
    2. Install and configure the new project using the State Tool. 

## Updating existing projects

To update an existing project using `requirements.txt`:

1. Navigate to the Python project you want to update.
2. Click the **Configuration** tab.
2. Click **Import from requirements.txt**  in the **Requested Packages** panel.
3. Open the `requirements.txt` to use and copy and paste the content, or type in your requirements individually.

![requirements.txt](../../images/requirements-txt.png "requirements.txt entries for import")

4. Click **Import**.

## requirements.txt syntax

* You must specify one requirement per line.
* You can specify just the package name and let the Platform choose the version each time a build is created. The Platform will choose the latest version, unless a different version is required based on the other packages included in the project.
* You can provide requirement specifiers for individual packages using the standard `pip` requirement specifier syntax:

Requirement specifier | Name | Description 
|----|----|----|
`==` | Equal to | An exact match is required.<br>requests==2.18.4
`>` | Greater than | Use any version greater than the specified version.<br>requests>2.18.4
`>=` | Greater than or equal to | Use any version greater than the specified version.<br>requests>=2.18.4
`<` | Less than | Use any version less than the specified version.<br>requests<2.18.4
`<=` | Less than or equal to | Use any version less than or equal to the specified version.<br>requests<=2.18.4
`~=` | Compatible version | Use any version greater than or equal to the specified version, but not greater than the current release series.<br>~=1.4.2 matches 1.4.2 through 1.4.9) but does not match 1.5.0

{{% notice note %}}
Some requirement specifier syntax is not applicable to the ActiveState Platform and is not supported:

* Environment markers (e.g. `SomeProject ==5.4 ; python_version < '2.7'`) are not supported. Instead, you should specify the appropriate package requirement specifier for your Platform project's Python version.
* Direct references (e.g. `SomeProject @ file:///somewhere/...`) are not supported because all of the requirements for a Platform project must come from the Platform.
{{% /notice %}}
