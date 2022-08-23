+++
date = "2022-08-22"
title = "Git Error:Password Authentication"
description = "An error occured when git push"
slug = ""
authors = ["Shane"]
tags = ["Git"]
categories = ["Git"]
externalLink = ""
series = []

+++
## Description:
    remote: Support for password authentication was removed on August 13, 2021.
## Solution:
    Use token other than password to log in.
* Go to github->settings->Developer Settings->personal access tokens
* generate new tokens, save it.
* When you push new commit, enter the token other than your password
