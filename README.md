# Contactify-CI

This repository contains reusable workflows for our Continuous Deployment and Delivery.

## Overview

### shared-test.yml

This workflow can be used to run our nx based frontend tests.

_Currently (2022-11-21) it only runs the build, as there is no test setup yet._

### shared-load-matrix.yml

This workflow allows to load a json file minified into a variable. This can then be used to dynamically populate the Build Matrix.

### shared-deploy.yml

This workflow publishes the nx frontend to an Azure AppService. It receives a Docker image reference and updates the specified deployment with that image.

### shared-deploy-pr.yml

This workflow publishes the nx frontend to an Azure AppService Slot. It receives a Docker image reference, creates a deployment slot of the specified application (based on the github event number) and deploys the image to that slot.

### shared-build-docker.yml

This workflow builds a docker image of the specified nx application. It outputs the image reference to be used by another job (eg. `shared-deploy.yml`).

Tags that will be created:

Event | Tags
--- | ---
Push to branch (mostly `develop`, depends on upstream) | `latest-<variant>-development`
Tags `release**` | `latest-<variant>`, `<tagname>-<variant>`
Pull request | `review-pr-<pr-number>-variant`

### shared-build-and-deploy.yml

This workflow calls the `shared-build-docker.yml` and `shared-deploy.yml` workflows to deploy the specified application to the specified Azure AppService.

### shared-build-and-deploy-pr.yml

This workflow calls the `shared-build-docker.yml` and `shared-deploy-pr.yml` workflows to deploy the specified application to an Azure AppService Slot, which it also creates based on the github event number.

## Authentication

To allow these workflows to update the deployments, we use "Federated Credentials". You find mor information here: https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect or in the wiki: https://contactify-ag.atlassian.net/wiki/spaces/DBC/pages/232423446/Deployments