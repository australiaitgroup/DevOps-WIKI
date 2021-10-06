# Docker CLI
## tool: docker

# Build docker image and Run in a container
## tools: Dockerfile
Format
Syntax
Environment variables
https://docs.docker.com/engine/reference/builder/#environment-replacement
### Question:
1. why web services can run automatically on a container without entrypoint?
[CMD .sh]:(https://github.com/tiangolo/uwsgi-nginx-flask-docker/blob/master/docker-images/python3.7.dockerfile) => [supervisord]:(https://github.com/tiangolo/uwsgi-nginx-docker/blob/master/docker-images/start.sh)
[supervisord-alpine.ini]:(https://github.com/tiangolo/uwsgi-nginx-docker/blob/master/docker-images/supervisord-alpine.ini)
# Push images to Docker Hub/registry(configured by yourself or organisation)

# Build and Run Multi-continers

# Case Study
## Container-based CI/CD by GitHub Action pipline

https://docs.docker.com/ci-cd/github-actions/
