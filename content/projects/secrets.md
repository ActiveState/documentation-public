---
title: Adding Secrets to your project
---

Secrets are for sensitive information that needs to be shared between environments and people working on a project. For example, you can securely store API keys and database passwords using secrets. Secrets are client-side encrypted values, meaning that they are not stored on our servers and ActiveState cannot access your secret values.

To add a secret to your project:

1. In **Your Dashboard**, select the organization that contains the project you want to add a secret to and then click the **Projects** tab, or click the **Projects** tab in your dashboard to add a secret to a personal project.
2. Click the project to open.
3. Click the **Scripts** tab.
4. Click **Secrets** in the **Scripts** menu.
5. Click **Add a Secret**.
6. Enter a name for the secret, and optionally enter a description.
7. Select the scope of the secret:
    * **Project**: The secret is visible to all users who have permissions to activate the project. The value of the secret is shared between members of the organization.
    * **User**: Each user sets their own value and only that user can see it.
8. Click **Add Secret**.

When you activate a project that contains a secret with no value defined, you will be prompted for the value. Alternatively, click on the arrow next to the secret name on the **Secrets** page to expand the instructions for setting the secret value manually using the State Tool.
