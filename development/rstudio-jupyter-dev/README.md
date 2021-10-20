# RStudio for JupyterHub
A dockerized [RStudio](https://www.rstudio.com/products/rstudio/download-server/) instance for [JupyterHub](https://github.com/jupyterhub/zero-to-jupyterhub-k8s) on Kubernetes

> note see [jupyter-r-notebook](https://hub.docker.com/r/jupyter/r-notebook)

You can use this package in any jupyter hub environment

## Contents
There are 2 packages pre-installed on the Rstudio.
- [dsBaseClient](https://github.com/datashield/dsBaseClient/tree/x.x-dev)=x.x-dev
- [dsHelper](https://github.com/lifecycle-project/ds-helper)=x.x.x

Additional packages that you need for a workshop for example.
- [tidyverse](https://www.tidyverse.org/packages/)

## Usage
You can use the image locally as well. Run the following snippet:

`docker run -p 8787:8787 datashield/rstudio-jupyter:latest -d`

You can access rstudio on http://localhost:8787
### Authentication
We authenticate with the central authentication mechanism of [MOLGENIS](https://molgenis.org) and [ELIXIR](https://elixir-europe.org/services/compute/aai).