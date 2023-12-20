---
icon: material/open-in-app
title: "Deploying the Glean Browser Extensions"
description: "The Glean Browser extension can either be manually installed by your users or pushed to managed devices by your admins."
lang: en
tags:
    - "administration"
    - "deployment"
    - "extension"
authors:
  - Cindy Chang
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1319GHNUoLQhSHuBXLrSEgwaeTzIeEIi5z3cx9uT5zIY/edit
  - https://help.glean.com/en/articles/3643252-installing-the-browser-extension
  - https://help.glean.com/en/articles/7960475-steps-to-enable-managed-chrome-push
  - https://help.glean.com/en/articles/7915618-managed-chrome-extension-rollout#h_230c1655eb
---

The Glean Browser extension can either be manually installed by your users or pushed to managed devices by your admins.

## Deploying to Managed Devices

=== "Managed Chrome"
    To facilitate adoption and usage, a company-managed rollout of the Glean Chrome extension can be pushed to all employees. This means all employees will automatically have Glean’s Chrome extension installed on company-managed computers.

    Users will not be able to disable/uninstall the extension if it is installed through Managed Chrome.

    **Installation**

    1. Ensure you have or work with someone who has Google Workspace Admin privileges.
    2. Go to [https://admin.google.com/ac/chrome/apps/user](https://admin.google.com/ac/chrome/apps/user){:target="_blank"}
    3. Use the left bar to choose the organizational unit you would like to deploy the extension to.

        !!! tip
            Even if the extension is being rolled out company-wide, it is a good idea to select a company-wide organizational unit so that the extension will only be pushed on the Chrome profile associated with employees' work accounts.
    4. Hover over the + button in the bottom right corner and select "**Add from Chrome Web Store**".
    5. Search for “Glean” and select the option corresponding to the Glean work extension.
    6. Click **Select** at the top-right. When the extension appears, click on it to open the right nav bar.
    7. In **Policy for extensions** enter:
        ```
        { "BaseUrl": { "Value": "https://<INSTANCE_NAME>-be.glean.com" }}
        ```
        To confirm your instance name, please contact Glean support.
    8. Click **Save**.
    9. Hover over the **Installation Policy** for the extension and select either **Force Install** or **Force Install + pin to browser toolbar**.
    10. Click **Save**.
    
    !!! success
        You’re all set!
        
        There may be a delay on the Google/Chrome side for when the extension is pushed. Expect all employees to have the extension present within 24-48 hours.


=== "Managed Edge"
    To facilitate adoption and usage, the Glean Edge extension can be pushed by company admins to all managed devices. Users will not be able to disable/uninstall the extension if it is installed through Managed Edge / Group Policy.

    You can use the [ExtensionInstallForceList](https://learn.microsoft.com/en-us/DeployEdge/microsoft-edge-policies#extensioninstallforcelist){:target="_blank"} policy to install the Glean extension silently.

    **Installation**

    1. In the Group Policy Editor, go to **Administrative Templates** > **Microsoft Edge** > **Extensions** > and then select **Control which extensions are installed silently**.

    2. Select **Enabled**.

    3. Click **Show**.

    4. Enter the following ID to install the Glean extension from the Chrome web store:
        ```
        cfpdompphcacgpjfbonkdokgjhgabpij;https://clients2.google.com/service/update2/crx
        ```

    !!! success
        You're all set!

        The extension is installed silently without user interaction. The user also won't be able to uninstall or disable the extension. This setting overwrites any blocklist policy that is enabled.


## Deploying to Unmanaged Devices
The Glean Browser Extension can be directly installed by users manually at the following links:

* :fontawesome-brands-chrome: [Chrome](https://chrome.google.com/webstore/detail/glean/cfpdompphcacgpjfbonkdokgjhgabpij){:target="_blank"}
* :fontawesome-brands-firefox: [Firefox](https://addons.mozilla.org/en-US/firefox/addon/glean/){:target="_blank"}
* :fontawesome-brands-edge: [Edge](https://chrome.google.com/webstore/detail/glean/cfpdompphcacgpjfbonkdokgjhgabpij){:target="_blank"}
    * The enable the [Allow extensions from other stores](https://support.microsoft.com/en-us/microsoft-edge/add-turn-off-or-remove-extensions-in-microsoft-edge-9c0ec68c-2fbc-2f2c-9ff0-bdc76f46b026){:target="_blank"} setting must be enabled.
* :fontawesome-brands-safari: [Safari](https://apps.apple.com/us/app/glean-for-safari/id6444195239?mt=12){:target="_blank"}
* :simple-brave: [Brave](https://chrome.google.com/webstore/detail/glean/cfpdompphcacgpjfbonkdokgjhgabpij){:target="_blank"}


## Email Template
Refer to below email template below for a company-wide communication to inform of a managed Chrome/Edge install.


> **Subject: New browser extension available for all employees**

> *Title: Key updates to your browser*

> In [company name]’s continued effort to support employee well-being and productivity, we are rolling out a new company-wide search tool, [Glean](https://www.glean.com/).

> Using Glean, you can search across all work applications we use at [company name]. Whether the document or answer you are looking for lives in [GDrive, Slack, Email, Jira *customize with your company's tools] or with another colleague, Glean will help you search for and discover what you need to get your work done. All without remembering where all your documents are hosted or messaging multiple people. 

> Starting [launch date], Glean will be installed on your Chrome browser. Note that this launch will replace your current default new tab page with Glean so you can easily [access search across all apps](https://help.glean.com/en/articles/4712824-search-from-wherever-you-work). 