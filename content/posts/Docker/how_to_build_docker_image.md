+++ 
date = 2022-08-24
title = "Docker Error: Build a docker image"
description = "Differencce between `RUN` and `CMD`"
slug = ""
authors = ["Shane"]
tags = ["Docker"]
categories = ["Virtualization"]
externalLink = ""
series = []
+++

I have a simple python web application imported `flask` and I want to build it as a image. I followed some tutorial.
## Steps to build a docker image
1.  Create a new file names `Dockerfile` in the root folder you want to package.
2.  Config the file<br /> 


    `From python:3.10`<br />

    `ADD main.py`<br />

    `RUN pip install Flask`<br />

    `EXPOSE 8080`<br />

    `CMD [ "python", "./main.py" ]`<br />

I used `CMD ['pip install Flask']`at first which generated error:<br >`ModuleNotFoundError: No module named 'flask'` 

## Difference between `RUN` and `CMD`
|RUN|CMD|
|---|---|
|Execute any commands in a new layer on top of the current image|Provide defaults for an executing container|
|The resulting committed image will be used for the next step in the Dockerfile|Can only be one CMD instruction in a Dockerfile. If you list more than one CMD then only the last CMD will take effect.|

* As shown above, `RUN` command is used to  provide prerequesite for the next layer in image. 
* While `CMD` provide default arguments for a running container. `CMD` works as what is input after `exec` the container. 
* In our case, flask is the prerequisite for the folowing python command. So we need to `RUN` it.

## Reference
> https://docs.docker.com/engine/reference/builder/#cmd