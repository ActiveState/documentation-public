---
title: Troubleshooting
---

* [Troubleshooting FAQ](#troubleshooting-faq)
* [Reporting Errors](#reporting-errors)

## Troubleshooting FAQ

**Can I pass my invite on to someone else in my organization?**

No. The invite email is specific to your email address and your organization. If you would like to provide access to other people in your organization you can either 1) sign up for the Platform yourself and invite them, or 2) contact us with the email addresses of the users to invite, and we will send them individual invites. 

**My invite link URL points to the http://t.yesware.com domain. Is this spam? Why doesn't it come from your company's usual activestate.com mail server?**

No, the email is from ActiveState. We used Yesware, a third party service to mail merge and send the Platform invite emails. If your network rejects emails sent via Yesware, contact us and we will send you an invite directly from the platform.

**Why am I not notified that the My Account site, located at [https://account.activestate.com](https://account.activestate.com), is scheduled to shut down when I log in there?**

My Account should display this messaging, and it will be added soon.

## Reporting Errors

### Browser errors

As you work in the ActiveState Platform you may encounter temporary issues due to network or Internet connectivity problems. The majority of the time these issues will resolve themselves promptly and you can continue by waiting for a short period of time and then refreshing the page, or by closing your browser or logging out and then signing in again.

If however you consistently encounter an error message, you can help us diagnose the problem by checking for errors in your browser before contacting the support team. 

You can do this by opening your browser's developer tools and taking a screenshot of any errors displayed in the console, or site log window. In most browsers, you can access the console by right clicking on the web page displaying the error and selecting **Inspect**.

In some browsers, opening the developers tools might not automatically display the console. If this happens, click the Console option in the developer window and take screenshots of any errors displayed there.

Please reach out to the support team at <a href="mailto:support@activestate.com">support@activestate.com</a> with the error screenshots, along with:

* The email address associated with your ActiveState Platform account 
* The specific browser and version combination you are using to access the Platform.
* Your operating system and version.

For more detailed information about using the developer tools in your browser, see the browser documentation:

* [Chrome](https://developers.google.com/web/tools/chrome-devtools/?hl=en)
* [Internet Explorer](https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/samples/gg589512(v=vs.85)#OpeningTools)
* [Microsoft Edge](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide/console)
* [Firefox](https://developer.mozilla.org/en-US/docs/Tools/Web_Console/Opening_the_Web_Console)
* [Safari](http://www.technipages.com/mac-os-x-enable-web-inspector-in-safari)

### State Tool issues

If you encounter errors when using the State Tool, please reach out to our support team at <a href="mailto:support@activestate.com">support@activestate.com</a>. The more information you can provide them with, the sooner your issue can be reproduced and resolved. Please provide the following information, where possible:

* A short summary of the issue
* Step steps to reproduce
* Expected result
* Actual result
* Logs (if relevant)

The State Tool logs are stored in the following locations by default:

* Windows: `C:\Users\<User>\AppData\Roaming\activestate\cli-unstable\log.txt`
* Linux: `~/.config/activestate/cli-unstable/log.txt`
