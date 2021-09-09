# Jupyter Notebook RStudio containers
We are using Jupyter Notebooks to configure the different clients of DataSHIELD packages used in the projects we serve.

Currently we support these analysis environments:

Production
- DataSHIELD base environment [dsBase](https://github.com/datashield/dsBaseClient)
- Exposome environment [dsExposome](https://github.com/isglobal-brge/dsExposomeClient)

Development
- DataSHIELD Base development environment [dsBase](https://github.com/datashield/dsBaseClient) --> master branch

You can you these images to support different analysis environments on the JupyterHub.
## Development
We define 2 environment in development of these images.

- production == R-packages can be used as production environments on JupyterHub
- development == R-packages are not released yet and/or work only with the development version of the dsBaseClient or other packages

## Building and publishing
We use [semantic release](https://github.com/semantic-release/semantic-release) to build and release the images.
