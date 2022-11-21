# Contactify-CI

This repository contains reusable workflows for our Continuous Deployment and Delivery.

## Overview

### shared-test.yml

This workflow can be used to run our nx based frontend tests.

_Currently (2022-11-21) it only runs the build, as there is no test setup yet._

### shared-load-matriy.yml

This workflow allows to load a json file minified into a variable. This can then be used to dynamically populate the Build Matrix.

### shared-deploy.yml

This workflow publishes the nx frontend to an Azure AppService. It receives a Docker image reference and updates the specified deployment with that image.

### shared-deploy-pr.yml

This workflow publishes the nx frontend to an Azure AppService Slot. It receives a Docker image reference, creates a deployment slot of the specified application (based on the github event number) and deploys the image to that slot.

### shared-build-docker.yml

This workflow builds a docker image of the specified nx application. It outputs the image reference to be used by another job (eg. `shared-deploy.yml`).

Tags that will be created:
_TBD_

### shared-build-and-deploy.yml

This workflow calls the `shared-build-docker.yml` and `shared-deploy.yml` workflows to deploy the specified application to the specified Azure AppService.

### shared-build-and-deploy-pr.yml

This workflow calls the `shared-build-docker.yml` and `shared-deploy-pr.yml` workflows to deploy the specified application to an Azure AppService Slot, which it also creates based on the github event number.
