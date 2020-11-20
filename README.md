# Refgenieserver deploy guide

We're running 4 server instances on an AWS ECS cluster. These are available at:

## Primary server

- service-name: rgs-service-primary
- url: http://refgenomes.databio.org
- repository: http://github.com/refgenie/refgenomes.databio.org
- update: The primary server is deployed with change to the `config/refgenie_config_archive.yaml` on master branch. It uses the `docker.io/databio/refgenieserver:latest` image as base.

## Data staging

- service-name: rgs-service-software-staging
- url:  http://rg.databio.org:81
- repository: http://github.com/refgenie/data_staging
- update: The data-staging server is deployed push to master branch of the data_staging repository
- description: Uses the release software to show how some new test data would render.

## Software staging

- service-name: rgs-service-data-staging
- url:  http://rg.databio.org:82
- repository: http://github.com/refgenie/refgenieserver 
- update: The software-staging server is deployed on push or PR to the staging branch. It deploys to `docker.io/databio/refgenieserver:staging`.
- description: Uses the released data to show how new software would render.

## Basic demo

- service-name: rgs-service-demo
- url:  http://rg.databio.org:83
- repository: http://github.com/refgenie/server_deploy_demo
- update: Deployed with change to the config archive file in `/config`.
- description: This is a basic self-contained demo that shows the entire process, from data to AWS container service.

## Two-stage container strategy

We use a 2-stage container building strategy:

1. we build the refgenieserver application with no data, which lives at docker.io/databio/refgenieserver.
2. for deploying a server, we start from the docker.io/databio/refgenieserver image and add a config file, building a new image that we can then deploy.

