---
title: "Security and Compliance"
weight: 5
---

 Security & Compliance enables you to automatically identify out-of-date or unsecure Python packages running in your environment. To begin, you need to complete a few configuration steps to specify the applications to scan and how to organize the scan results in the Platform.

Note: The **Security & Compliance** tab provides access to the security features of the Platform. It is available for Organizations on the Business and Enterprise tiers.

### Configuring Security & Compliance

Security & Compliance requires configuration to map the ActivePython interpreter you want to scan for vulnerabilities with the identity in the ActiveState Platform where you want to record the packages scanned and any details for any vulnerabilities identified.

1. Create an identity: An identity is a tracking identifier that organizes the results of security scans performed for one or more Python interpreters. For example, you could create a "Development" identity to track all security scans performed on development servers.

    1. Select an organization in the **Your Organizations** list.
    1. Click the **Security & Compliance** tab.
    1. Click **Identities**.
    1. Enter a meaningful name for the identity and click **Create**.
    1. Create a new plain text file with the contents of the sample configuration file and save it as `activestate.config`. For more information, see [Configuring Identities](/security/create_config.html) and [Where to place your `activestate.config` file?](/security/config_placement.html).

1. Download the Security & Compliance plugin

    1. In the Security & Compliance tab, click **Get Started**.
    2. Click the **ActiveState-SecurityScanner-0.5.5** button to begin the download.


1. Configure the Security & Compliance plugin on systems where interpreters run that you want to record scan data for. This involves two configuration steps:

    1. Use the `pip` package manager to install the plugin. For example, for Python3 with `pip3` installed, at the command prompt where you downloaded the plugin enter: `python3 -m pip install ActiveState-SecurityScanner-0.5.1.tar.gz`
    For more detailed instructions, see [Installing the Security & Compliance Plugin](/security/install).
    1. Download the `activestate.config` file to direct your security scan output to a specific identity. For details, see [Configuring Identities](/security/create_config.html) On Linux or macOS, copy the file to the `/etc` directory if you want all security scans run on that computer to use the same identity. On Windows, create an `ACTIVESTATE_CONFIG` environment variable that points to your `activestate.config` file. For more information on configuration options, see [Configuring Identities](/security/config_placement.html).

1. Run your applications and scripts with ActivePython interpreters that have the Security & Compliance plugin installed, and then check the **Dashboard** to see updates in **Your Latest Activity**. When the first security scan is complete you can view details in **Security & Compliance** tab for the organization associated with the identity.  