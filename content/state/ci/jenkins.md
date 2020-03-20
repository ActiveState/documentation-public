---
title: "Jenkins"
---

The following sections describe the tasks you need to complete to set up a CI/CD process with Jenkins, your version control system (VCS), and the ActiveState Platform. You need the appropriate access to these systems to complete the setup. In the examples below, we show configuration steps for GitHub specifically. You may need to adjust some of the tasks if you are using a different VCS. 

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

## Jenkins setup

1. Navigate to the web console for your Jenkins instance.
2. Click **New Item**, enter a name for your new item, and then choose **New Pipeline** and click **OK**.
3. In the **Build Triggers** section, choose **GitHub hook trigger for GITScm polling**. This setting combined with the [Webhook setup](#webhook-setup) task will cause a new build to run each time changes are pushed to the code repository. 
4. In the **Pipeline** section, select **Pipeline script from SCM** as the **Definition**.
5. Select Git or Subversion as your version control system and enter the **URL** for your repository.
6. Click **Add** > **Jenkins** to add your ACTIVESTATE_API_KEY and enter the following settings:

    - **Kind**: Secret text
    - **Secret**: The API key generated in [Obtaining your API key](#obtaining-your-api-key).
    - **ID**: ACTIVESTATE_API_KEY<BR><BR>
    ![](/images/jenkins-api-key.png)

7. If you want to use secrets, click **Add** > **Jenkins** to add your ACTIVESTATE_PRIVATE_KEY and enter the following settings:

    - **Kind**: Secret text
    - **Secret**: The contents of your private.key file from [Obtaining your private key](#obtaining-your-private-key)
    - **ID**: ACTIVESTATE_PRIVATE_KEY

    **NOTE**: In some cases you may need to escape certain characters in your private key. 

    You need to open the `private.key` file and copy the contents.

    ```text
    -----BEGIN RSA PRIVATE KEY-----
    ...
    3W5OE+S83fcBz1u7pNzgE4UtXJOADW0PtGt7dLnxqxWJbg38mKYMmqwDoD3/HkfH
    ...
    -----END RSA PRIVATE KEY-----
    ```

8. If you are setting up a private repository, you will need to configure access for the repository for Jenkins.

![Jenkins pipeline setup](/images/jenkins-pipeline-setup.png)

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

## Add a Jenkinsfile

You need to add a `Jenkinsfile` to the root of your code repository that includes all of the steps required to build, test, and deploy your code. The example provided demonstrates the State Tool-specific steps for installing the State Tool and running scripts that are defined in the `activestate.yaml` file for the project.

```text
pipeline {
    agent any

    environment {
        // Bash is one of the state tool's supported shells. Jenkins defaults 
        // to sh so we have to set it explicitly here
        SHELL="/bin/bash"

        // Since jobs run as the user 'jenkins' we do not have permission
        // to install the state tool anywhere on the current PATH. We 
        // instead update the path here to a known location that we
        // will install to
        PATH="$WORKSPACE:$PATH"
        ACTIVESTATE_API_KEY = credentials('ACTIVESTATE_API_KEY')
    }

    stages {
        stage ('Environment') {
            steps {
                sh 'env'
            }
        }
        stage ('Install state tool') {
            steps {
                sh'''
                curl -q https://platform.activestate.com/dl/cli/install.sh -o install.sh
                chmod +x install.sh
                ./install.sh -n -t $WORKSPACE || true
                '''
            }
        }
        stage ('Print location of Python interpreter') {
            steps {
                sh 'state run which-python'
            }
        }
        stage ('Active private project and run script') {
            steps {
                sh 'state run clean'
            }
        }
        stage ('Cleanup') {
            steps {
                sh 'rm -rf ~/.cache/activestate'
                sh 'rm install.sh'
                sh 'rm -rf state'
            }
        }
    }
}
```

The scripts being executed in the `Jenkinsfile` are defined in the scripts section of the `activestate.yaml` file for the project:

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

## Webhook setup

If you want Jenkins to create a new build each time code changes are checked in to your repository, you need to set up a webhook in the GitHub settings for your repository. The webhook posts a message to Jenkins each time changes are pushed to the repository with the information required for Jenkins to start the associated build.

1. Open your web browser and navigate to your repository on github.com.
2. Click **Settings**.
3. Click **Web Hooks**, and then click **Add Webhook**.
4. In **Payload URL**, enter the URL for your Jenkins instance with the path `/github-webhook/`. For example: `https://jenkins.acme-tech.com/github-webhook/` 

![Jenkins Github webhook](/images/jenkins-github-webhook.png)

If your Jenkins pipeline is configured correctly, you will see a job start and complete successfully each time someone pushes new code changes to the repository.

![](/images/jenkins-build-states.png)
