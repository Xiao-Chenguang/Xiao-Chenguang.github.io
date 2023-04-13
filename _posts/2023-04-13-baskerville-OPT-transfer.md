---
layout: post
title:  "Transfer Micrisoft Authentication OPT for baskerville from one phone to another"
date:   2023-04-13
categories: skills
author: Chenguang Xiao
---

<!-- # Transfer Micrisoft Authentication OPT for baskerville from one phone to another -->

One receiving the new iphone, data from the old phone are the most important thing to be keeped.
There is any easy way to do this from iphone to iphone with 'quick start' feature.
However, there is do not help with the otp authentication for baskerville and maybe all other organization accounts.

## Workarounds provided by Microsoft Authenticator

There is acutally a way to transfer the otp authentication from one phone to another.
That is export and import save ID from Microsoft Authenticator settings.

### Steps to export and import save ID

+ click the button on the left upper corner of the Microsoft Authenticator app
+ find and click the button 'Settings'
+ find and click the button 'Export save ID' at the bottom of the page
+ save the file to your iclout drive(create a folder first is recommended)
+ the key file is end with '.jwt'

The you can recover the saved otp authentication from the key file on your new phone:
+ follow the previous steps to open the settings page and click the button 'Import save ID' instead
+ select the key file you saved before
+ your OTP is transfered to your new phone successfully

Then you can check the otp code on both phones to ensure they are the same.