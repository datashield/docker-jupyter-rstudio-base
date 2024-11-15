# RStudio for JupyterHub
A dockerized [RStudio](https://www.rstudio.com/products/rstudio/download-server/) instance for [JupyterHub](https://github.com/jupyterhub/zero-to-jupyterhub-k8s) on Kubernetes

> note see [jupyter-r-notebook](https://hub.docker.com/r/jupyter/r-notebook)

You can use this package in any jupyter hub environment

## Contents
This profile is make with the [xenon](https://www.datashield.org/help/standard-profiles-and-plaforms#athlete) packages 

## Usage
You can use the image locally as well. Run the following snippet:

`docker run -p 8787:8787 datashield/rstudio-jupyter:latest -d`

You can access rstudio on http://localhost:8787
### Authentication
We authenticate with the central authentication mechanism of [MOLGENIS](https://molgenis.org) and [ELIXIR](https://elixir-europe.org/services/compute/aai).