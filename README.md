# Refgenieserver deploy guide

We're running 4 server instances on an AWS ECS cluster. These are available at:
- http://rg.databio.org (primary)
- http://rg.databio.org:81 (data-staging)
- http://rg.databio.org:82 (software-staging)
- http://rg.databio.org:83 (demo)

Repos that auto-deploy containers to these servers are:

- http://github.com/refgenie/refgenomes.databio.org (primary). The primary server is deployed with push to master branch.
- http://github.com/refgenie/data_staging (data-staging). The data-staging server is deployed push to master branch of the data_staging repository
- http://github.com/refgenie/refgenieserver (software-staging). The software-staging server is deployed push or PR to staging branch
- http://github.com/refgenie/server_deploy_demo (demo). Deployed with push to master branch.

## Two-stage container strategy

We use a 2-stage container building strategy:

1. we build the refgenieserver application with no data, which lives at docker.io/databio/refgenieserver.
2. for deploying a server, we start from the docker.io/databio/refgenieserver image and add a config file, building a new image that we can then deploy.

