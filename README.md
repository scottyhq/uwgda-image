# UWGDA2020 JupyterHub Image Builder

This repository builds a [JupyterHub](https://jupyter.org/hub) environment with [Repo2Docker](https://repo2docker.readthedocs.io/en/latest/) and [GitHub Actions CI](https://help.github.com/en/actions/automating-your-workflow-with-github-actions) 

[![Action Status](https://github.com/UW-GDA/uwgda-image/workflows/Repo2Docker/badge.svg)](https://github.com/UW-GDA/uwgda-image/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/UW-GDA/uwgda-image)](https://hub.docker.com/r/UW-GDA/uwgda-image/tags)

https://hub.docker.com/r/UW-GDA/uwgda-image/tags

### How to use

build with GitHub Actions simply by pushing to GitHub

* pull requests trigger image building without pushing to DockerHub

* commits to master branch (except readme.md changes) trigger re-building image 
* successfully built image is tagged by github commit short sha and 'latest'
```
git commit -a -m "modified binder/environment to my liking"
git push
```
* pushing a tag results in a docker image with the same tag:
```
git tag -am "tag version 2019.1" 2019.1 
git push --tags
```

### Pull your image to run a local JupyterLab session
```
export IMAGE=UW-GDA/uwgda-image
export TAG=latest
docker pull 
docker run -it --name UW-GDA -p 8888:8888 $IMAGE:$TAG jupyter lab --ip 0.0.0.0
docker stop UW-GDA
docker rm UW-GDA
```

### Point to a specific tagged image in JupyterHub config
(image: UW-GDA/uwgda-image:2019.1)
https://zero-to-jupyterhub.readthedocs.io/en/latest/reference/reference.html?highlight=profile_list#singleuser-profilelist

