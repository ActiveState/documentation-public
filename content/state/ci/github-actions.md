---
title: "GitHub Actions"
---

The following sections describe the tasks you need to complete to set up a CI/CD process for a Python project with GitHub, GitHub Actions, and the ActiveState Platform.

## Gathering environment variable settings

**Before you begin**: 

* You need an ActiveState Platform account. If you do not currently have an account you can sign up for free at: [https://platform.activestate.com/create-account](https://platform.activestate.com/create-account). 
* You need to have the State Tool installed on your computer, and authorized with the Platform using the `state auth` command, in order to run the command to retrieve the API key, and to access your `private.key` file if you are using secrets.

The State Tool will use the following environment variables if they are defined:

- **ACTIVESTATE_API_KEY**: This API key is used to authenticate the State Tool with the ActiveState Platform, as required, to download language projects, update packages, etc. If you use ActiveState Platform secrets in your build process or scripts run by the build process, you must also configure the ACTIVESTATE_PRIVATE_KEY.
- **ACTIVESTATE_PRIVATE_KEY**: Optional. The private key to use for decrypting secrets.

### Obtaining your API Key

Currently, you can only generate an API Key by calling our API directly using a `curl` command. Open your command prompt, and copy and paste or enter the following command: 

```text
curl -X POST "https://platform.activestate.com/api/v1/apikeys" \
-H "accept: application/json" -H "Content-Type: application/json" \
-H "Authorization: Bearer `state export jwt`" \
-d "{ \"name\": \"APIKeyForCI\"}"
```

Example response:

```text
{
  "name": "APIKeyForCI",
  "token": "MjZlMGI5YzQtYzFkMS00MmUxLTllYjAtODRjMjA5YzVjZTNmXlFhQ3llUW9WeGlzaTUxNzku",
  "tokenID": "26e0b9c4-c1d1-42e1-9eb0-84c209c5ce3f"
}
```

In this example, you would copy the token value to use as the ACTIVESTATE_API_KEY environment variable in your CI/CD application: `MjZlMGI5YzQtYzFkMS00MmUxLTllYjAtODRjMjA5YzVjZTNmXlFhQ3llUW9WeGlzaTUxNzku`

### Obtaining your Private Key

You can find the private key value at `<configdir>/activestate/cli-unstable/private.key`.

The configdir varies per platform, but in most cases will be at one of:

- Windows: `%HOME%\AppData\Roaming\activestate\cli-unstable\`
- Linux: `~/config/activestate/cli-unstable/`
- macOS: `~/Library/Application\ Support/activestate/cli-unstable/`

The private key environment variable expects the contents of the `private.key` file, not the filepath.

## GitHub setup

1. Sign in to GitHub and navigate to the repository where you want to add the GitHub Action.
2. Click **Settings**.
3. Click **Secrets** and then click **Add a new secret**.
4. In the **Secrets** page, click **Add a new secret** enter the name and value for each environment variable and click **Add secret**. For information on the required values, see [Generating an API key](#generating-an-api-key) and, if applicable, [Configuring your private key](#configuring-your-private-key).
**IMPORTANT**: The ACTIVESTATE_API_KEY is used to authenticate the State Tool automatically whenever required by the CI/CD build steps.<br><br>

![GitHub Action Secrets](/images/github-action-secrets.png)

If you're adding the ACTIVESTATE_PRIVATE_KEY environment variable, you need to open the `private.key` file and copy the contents.

```text
-----BEGIN RSA PRIVATE KEY-----
...
3W5OE+S83fcBz1u7pNzgE4UtXJOADW0PtGt7dLnxqxWJbg38mKYMmqwDoD3/HkfH
...
-----END RSA PRIVATE KEY-----
```

## ActiveState Platform project setup

You can use either the Dashboard or the State Tool to create a new project and add the language, platforms, and packages your project requires. Set up your project by:
    
* [Creating a new custom project](/projects/custom-builds/index.html)
* [Copying and editing (forking) an ActiveState project](/projects/forking/index.html)
* Use the [state init](/state/init.html) and [state packages](/state/packages.html) commands to create a new project and add the language, platforms (operating systems), and package requirements your code project needs. 

## Configure activestate.yaml

After you create an ActiveState project, complete the following steps to activate your project and add the configuration file to your code repository, so that the CI/CD has access to it.

1. Open your command prompt and navigate to the top level folder where you want to create your ActiveState Platform project.
2. Enter `state activate <owner/project_name>`. For example: `state activate acmetech/python-3-6-6`.
3. Copy the `activestate.yaml` configuration file to the root directory of your code repository.
4. Edit the `activestate.yaml` to add any scripts, variables, or secrets you want CI/CD to run or have access to. For more information on these options, see [Getting started](/state/start.html).
5. Add `activestate.yaml` to the repository and check in your changes.

## GitHub Action setup

1. Click the Actions tab.
2. Click **Set up a workflow yourself**.

    [Setup a workflow yourself](/images/github-actions-setup-workflow.png)
3. Replace the default script with State Tool specific configuration settings. The following example demonstrates how to install the State Tool on both Linux and Windows, and how to run scripts for linting the code and for tests using the State Tool.

    ```text
    # This is a basic workflow to help you get started with GitHub CI using ActivePython
    name: ActivePython application on GitHub CI

    # Setting up Cache directory and ActiveState Platform API key
    env:
      ACTIVESTATE_CLI_CACHEDIR: ${{ github.workspace }}/.cache
      ACTIVESTATE_API_KEY: ${{ secrets.ACTIVESTATE_API_KEY }}
      
    # Controls when the action will run. Triggers the workflow on push events on the default branch 
    on: [push]

    # A CI workflow  is made up of one or more jobs that can run sequentially or in parallel
    jobs:
      # This workflow contains a single job called "build"
      build:
        # The type of runner that the job will run on (this one is a matrix build)
        runs-on: ${{ matrix.os }}
        strategy:
          matrix:
            # Building on both Windows and Linux(Ubuntu) simultaneously 
            os: [windows-latest, ubuntu-latest]
        steps:
        # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
        - uses: actions/checkout@v2
        # Installing State Tool on Windows via Powershell 
        - name: Install State Tool (Windows)
          if: matrix.os == 'windows-latest'
          run: |
            (New-Object Net.WebClient).DownloadFile('https://platform.activestate.com/dl/cli/install.ps1', 'install.ps1'); 
            Invoke-Expression -Command "$Env:GITHUB_WORKSPACE\install.ps1 -n -t $Env:GITHUB_WORKSPACE"
            echo "::add-path::$Env:GITHUB_WORKSPACE"
        # Installing State Tool on Linux with default shell behavior
        - name: Install State Tool (Linux)
          if: matrix.os != 'windows-latest'
          run: sh <(curl -q https://platform.activestate.com/dl/cli/install.sh) -n
        # Checking ActiveState Platform for project updates
        - name: Update project
          run: state pull
        # Caching downloaded build using GitHub CI cache
        - name: Cache state tool cache
          uses: actions/cache@v1
          env:
            cache-name: cache-platform-build
          with:
            path: ${{ env.ACTIVESTATE_CLI_CACHEDIR }}
            key: ${{ runner.os }}-build-${{ env.cache-name }}-${{ hashFiles('activestate.yaml') }}
            restore-keys: |
              ${{ runner.os }}-build-${{ env.cache-name }}
        # Execute linting of the project on ActivePython
        - name: Lint with flake8
          run: state run lints
        # Running project tests using pytest on ActivePython
        - name: Test with pytest
          run: state run tests
    ```

    This setup should work for most Python projects with slight modifications. The YAML elements that could be tweaked include:

    * Update the **name** setting on line 2 to match your application
    * Update the **on** setting on line 10 to modify the triggers running the build (including setting the branch)
    * Update the operating systems in the  **matrix** section based on your target OS(es)
    * Replace the last two steps (lint and test) to match the specific script(s) to run for your project. The scripts you add must reference scripts defined in your `activestate.yaml` file.

4. Click **Start a Commit** and commit the Action configuration file to your repository. Each time you push changes to your code repository the CI/CD process install and launch the State Tool activated environment and run the scripts you have specified. 

You can view details for each time the workflow runs in GitHub by clicking the Actions tab, selecting the workflow, and then choosing clicking the title of the event to view. The logs for that event are then displayed.

![](/images/github-actions-logs.png)