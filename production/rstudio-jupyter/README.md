# RStudio for JupyterHub
A dockerized [RStudio](https://www.rstudio.com/products/rstudio/download-server/) instance for [JupyterHub](https://github.com/jupyterhub/zero-to-jupyterhub-k8s) on Kubernetes

> note see [jupyter-r-notebook](https://hub.docker.com/r/jupyter/r-notebook)

You can use this package in any jupyter hub environment

## Contents
There are 2 packages pre-installed on the Rstudio.
- [dsBaseClient](https://github.com/datashield/dsBaseClient/tree/6.1.0)=6.1.0
- [dsHelper](https://github.com/lifecycle-project/ds-helper)=0.0.0

## Usage
### Authentication
We authenticate with the central authentication mechanism of [MOLGENIS](https://molgenis.org) and [ELIXIR](https://elixir-europe.org/services/compute/aai).