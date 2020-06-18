# Refgenieserver deploy guide

We're running 3 server instances on an AWS ECS cluster. These are available at:
- http://rg.databio.org (primary server)
- http://rg.databio.org:81 (data staging server)
- http://rg.databio.org:82 (software staging server, with demo data)

Repos that auto-deploy containers to these servers are:

- http://github.com/refgenie/server_deploy_demo
- http://github.com/refgenie/server_deploy
- http://github.com/refgenie/refgenieserver

## Two-stage container strategy

We use a 2-stage container building strategy:

1. we build the refgenieserver application with no data, which lives at docker.io/databio/refgenieserver.
2. for deploying a server, we start from the docker.io/databio/refgenieserver image and add a config file, building a new image that we can then deploy.

## Deploy strategy

The demo data server (port 82) is deployed automatically with an update to the `master_archive.yaml` config file in the refgenie/server_deploy_demo repo.

It is also updated with a PR to the staging branch of refgenie/refgenieserver, which clones the demo.

The data staging server (81) is deployed automatically with update to the staging branch of the data repository, refgenie/server_deploy
