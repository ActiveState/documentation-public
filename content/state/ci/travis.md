---
title: "Travis"
---

The following sections describe the tasks you need to complete to set up a CI/CD process with Travis CI, your version control system (VCS), and the ActiveState Platform. You need the appropriate access to these systems to complete the setup. In the examples below, we show configuration steps for GitHub specifically. You may need to adjust some of the tasks if you are using a different VCS. 

{{% notice note %}}
Travis currently provides only limited support for Windows builds, and Windows configuration won't be covered in this guide. We'll add details for this configuration when Windows is fully supported on Travis CI.
{{% /notice %}}

## Gathering environment variable settings

**Before you begin**: 

* You need an ActiveState Platform account. If you do not currently have an account you can sign up for free at: [https://platform.activestate.com/create-account](https://platform.activestate.com/create-account). 
* You need to have the State Tool installed on your computer, and authorized with the Platform using the `state auth` command, in order to run the command to retrieve the API key, and to access your `private.key` file if you are using secrets.

The State Tool will use the following environment variables if they are defined:

* **ACTIVESTATE_API_KEY**: This API key is used to authenticate the State Tool with the ActiveState Platform, as required, to download language projects, update packages, etc. If you use ActiveState Platform secrets in your build process or scripts run by the build process, you must also configure the ACTIVESTATE_PRIVATE_KEY.
* **ACTIVESTATE_PRIVATE_KEY**: Optional. The private key to use for decrypting secrets.

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

* Windows: `%HOME%\AppData\Roaming\activestate\cli-unstable\`
* Linux: `~/config/activestate/cli-unstable/`
* macOS: `~/Library/Application\ Support/activestate/cli-unstable/`

The private key environment variable expects the contents of the `private.key` file, not the filepath.

## Travis setup

1. Log in to Travis CI at http://travis-ci.org for public or open-source repositories, or their paid option for private repositories at http://travis-ci.com.
2. Enable the repository you want to build.
    
    1. Select **Settings** from the top-right menu.
    2. Toggle the switch next to the repository you want to enable.
    3. Click **Settings** next to the repository you want to enable
    4. Under **Environment Variables**, enter the name and value for each API key you want to use and click **Add**. For information on the required values, see [Obtaining your API key](#obtaining-your-api-key) and, if applicable, [Obtaining your private key](#obtaining-your-private-key).
    
{{% notice info %}}
The ACTIVESTATE_API_KEY is used to authenticate the State Tool automatically whenever required by the CI/CD build steps.
{{% /notice %}}

![](travis-env-var.png)

{{% notice note %}}
In some cases you may need to escape certain characters in your private key. 
{{% /notice %}}

You need to open the `private.key` file and copy the contents.

```text
-----BEGIN RSA PRIVATE KEY-----
...
3W5OE+S83fcBz1u7pNzgE4UtXJOADW0PtGt7dLnxqxWJbg38mKYMmqwDoD3/HkfH
...
-----END RSA PRIVATE KEY-----
```

## ActiveState Platform project setup

You can use either the Dashboard or the State Tool to create a new project and add the language, platforms, and packages your project requires. Set up your project by:
    
* [Creating a new custom project](/projects/custom)
* [Copying and editing (forking) an ActiveState project](/projects/forks)
* Use the [state init](/state/commands/init) and [state packages](/state/commands/packages) commands to create a new project and add the language, platforms (operating systems), and package requirements your code project needs. 

## Configure activestate.yaml

After you create an ActiveState project, complete the following steps to activate your project and add the configuration file to your code repository, so that the CI/CD has access to it.

1. Open your command prompt and navigate to the top level folder where you want to create your ActiveState Platform project.
2. Enter `state activate <owner/project_name>`. For example: `state activate acmetech/python-3-6-6`.
3. Copy the `activestate.yaml` configuration file to the root directory of your code repository.
4. Edit the `activestate.yaml` to add any scripts, variables, or secrets you want CI/CD to run or have access to. For more information on these options, see [Getting started](/state/start).
5. Add `activestate.yaml` to the repository and check in your changes.

## Add a Travis configuration file

You need to add a `.travis.yml` file to the root of your code repository that includes all of the steps required to build, test, and deploy your code. The example provided demonstrates the State Tool-specific steps for installing the State Tool and running scripts that are defined in the `activestate.yaml` file for the project.

```text
# Install the State Tool as a dependency.
install:
  - sh <(curl -q https://platform.activestate.com/dl/cli/install.sh) -n

before_script:

# Run the linter and tests using the State Tool. Scripts named `lints` and `tests`
# must be defined in your project's activestate.yaml file. The ActiveState 
# Platform language runtime is downloaded and virtual environment is activated 
# when the first `state run` command is encountered. 
# In this case, `state run clean`  
script:
  - state run clean
  - state run which-python

# Turn email notifications off.
notifications:
  email: false
```

The scripts being executed in the `.travis.yml` file are defined in the scripts section of the `activestate.yaml` file for the project:

```text
scripts:
  - name: clean
    description: Run the data cleaner script
    value: python3 cleaner.py
  - name: which-python
    description: Determine which python interpreter is being used
    language: python3
    value: |
      import sys
      print("Python script running with: ", sys.executable)
```

If you successfully configured your Travis CI project, you will see a job start and complete successfully each time someone pushes new code changes to the repository.
