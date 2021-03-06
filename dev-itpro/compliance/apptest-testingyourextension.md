﻿---
title: "Testing your Extension"
description: "Describing the steps you must go through to successfully submit your app to AppSource."
author: SusanneWindfeldPedersen
ms.custom: na
ms.date: 01/11/2018
ms.reviewer: edupont
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: rweigel
---

# Testing your Extension

Several key things lead to your Business Central extension passing the Microsoft validation process. However, one of the most important checks you can do is to take the time and test your extension before submitting it for validation. This allows you to catch some of the basic errors that could lead to validation failures. The following list calls out key points, and the sections below provide more context.

- Always test in a [!INCLUDE[d365fin_long_md](../includes/d365fin_long_md.md)] online environment. If you test in an on-premises deployment, you might miss errors that would be seen online.
- Ensure that your extension can be published without code signing errors. You **must not** use the `-skipverification` flag.
- The extension should be able to be installed without errors.
- If you are using the **Assisted Setup**, ensure that you can use your wizard to completion without errors.
- Walk through the setup and usage of your extension to verify it works as expected (**remember to test as a user that does not have SUPER permissions**).
- Check that you can uninstall and unpublish your extension without any errors.
- Make sure you can republish and reinstall your extension without any errors.

## Use the correct Business Central version

Use Docker for your development and testing. At least, run your full test in Business Central online at least once before submitting for validation. We use Docker, and this ensures you will be testing on the same as what we validate your app on.  

If you test in an on-premises deployment, you might miss errors that would be seen online.

And with this, make sure you are using the correct Docker image tag to set up the correct Business Central version number. If you want your app to go live as soon as possible with the current production version at the time you submit your app, you must use the image tag mentioned at [Current Build - Developing for Dynamics 365 Business Central](https://partner.microsoft.com/en-us/dashboard/collaborate/packages/4756) on the Collaborate site. The image tag never changes and when we roll out a new version to production, the build underneath the image tag automatically changes for you. This means that you are always testing on current production.  
If you test on a build older or much newer, your app will most likely fail validation.

Use the image tag from the current build link above and make sure you refresh the docker instance each time you want to submit. If you haven’t run your docker script to refresh for months, then you are on a much older build.

## Use the correct data when you test your app

When we validate apps, we use the base CRONUS demo data. This of course is there for some countries and you don’t have to do anything additional to receive that demo data. However, for countries that are empty and don’t include demo data, you must import the CRONUS evaluation demo data. Not the International CRONUS data, the evaluation demo data. We do not use custom data and we do not use any other data. We always use the base evaluation demo data. To get this same data (if you don’t have it by default), you follow these instructions

1. Do a search for Configuration Packages, and then click it
2. Click Process > Import Predefined Package
3. Click the link for GB.ENU.EVALUATION

    That will start processing. You will see the process bar
4. If there are popups at all, just click Yes or OK
5. Once complete, click the Apply Package button
6. Click Yes
7. Again, if any popups or anything just click through them
8. Once it completes, you just sign out of Business Central and sign back in again
9. You now have data

## Use the right user for your testing

Do not do your testing with a user that has SUPER permissions marked. The SUPER user can do all without issue and you won’t catch your true app bugs. No live customer will have several users marked with this permission set. Therefore, we cannot test with it. You need to setup a user in your test environment that only has the BUS FULL ACCESS permission set, LOCAL, and any of your own permission sets. For information on how to setup this user, refer to this blog (you will want to use the user named ESSENTIAL)

## Testing your app

Now it is time to test your app. The following are all things you must do as part of your testing effort.

- Test your app in its entirety. We expect you to test 100% of the functionality of your app. Testing just a few areas of your app will not suffice. Test everything.
- We are not going to test 100% of the functionality of your app. We expect you to be doing that.
- If the testing works for you, it will most likely work for us
- Ensure that no permission errors are thrown for any of your app’s functionality
- With the ESSENTIAL user (before you assign your permission sets to it), make sure that the user can still use the core Business Central without facing permission errors. You must allow that user to do things such as accessing the Customer card, posting sales order, and so on.

## Maintaining your app

Although we do regular testing of your app when we prepare a new version of Business Central, we expect you to do the same on your end. You have access to the same builds that we do  through the Collaborate program. You can do more thorough testing than we can because you know your app the best. By doing this testing, you can catch future Business Central changes that may impact or break your app. Catching these changes in advance leaves less risk for customers to run into them.

You should be doing regular testing against our release branch that ports into our monthly service updates. To test against these builds, see [Daily Builds - Maintaining an app in AppSource for Dynamics 365 Business Central](https://partner.microsoft.com/en-us/dashboard/collaborate/packages/4754) on the Collaborate site.

We also recommend that you do regular testing against our release branch that eventually becomes our major release in April or October. For more information, see [Daily Builds - Developing for a future release of Dynamics 365 Business Central](https://partner.microsoft.com/en-us/dashboard/collaborate/packages/4755).

## See Also

[Checklist for Submitting Your App](../developer/devenv-checklist-submission.md)  
[Rules and Guidelines for AL Code](apptest-overview.md)  
