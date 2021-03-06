# UWGDA2020 JupyterHub Image Builder

This repository builds a [JupyterHub](https://jupyter.org/hub) environment with [Repo2Docker](https://repo2docker.readthedocs.io/en/latest/) and [GitHub Actions CI](https://help.github.com/en/actions/automating-your-workflow-with-github-actions)

[![Action Status](https://github.com/UW-GDA/uwgda-image/workflows/Repo2Docker/badge.svg)](https://github.com/UW-GDA/uwgda-image/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/uwgda/uwgda-image)](https://hub.docker.com/r/uwgda/uwgda-image/tags)

https://hub.docker.com/r/uwgda/uwgda-image/tags

### How to use

build with GitHub Actions simply by pushing to GitHub

* pull requests trigger image building without pushing to DockerHub
```
git clone https://github.com/UW-GDA/uwgda-image
cd uwgda-image
git checkout dev
# make sure dev branch is up-to-date with master
git merge master
# modify environment.yml or other files in binder/
git commit -a -m "modified binder/environment to my liking"
git push
# go to github.com and create a pull request to merge dev changes into master
```
* merged PRs or direct commits to master branch (changes to binder/* or requirements.txt) trigger re-building image
* successfully built image is tagged by github commit short sha and 'latest'
* pushing a tag to github results in a docker image with the same tag:
```
git tag -am "tag version 2020.1" 2020.1
git push --tags
```

### Pull your image to run a local JupyterLab session
```
export IMAGE=uwgda/uwgda-image
export TAG=2020.1
docker pull $IMAGE:$TAG
docker run -it --name UWGDA -p 8888:8888 $IMAGE:$TAG jupyter lab --ip 0.0.0.0
docker stop UWGDA
docker rm UWGDA
```

### Point to a specific tagged image in JupyterHub config
(image: uwgda/uwgda-image:2020.1)
https://zero-to-jupyterhub.readthedocs.io/en/latest/reference/reference.html?highlight=profile_list#singleuser-profilelist
