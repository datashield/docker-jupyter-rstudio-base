# RStudio - with dsMediationClient
Based upon [datashield/rstudio-jupyter](https://hub.docker.com/r/datashield/rstudio-jupyter). Extended with the dsMediation client environment.

## Contents
The exposome environment is pre-installed on the RStudio.
- [dsBaseClient](https://github.com/datashield/dsBaseClient/tree/6.1.0)=6.1.0
- [dsExposomeClient](https://github.com/datashield/dsMediationClient/tree/0.0.1)=0.0.1

## Usage
You can use the image locally as well. Run the following snippet:

`docker run -p 8787:8787 datashield/rstudio-jupyter-mediation:latest -d`

You can access rstudio on http://localhost:8787
### Authentication
We authenticate with the central authentication mechanism of [MOLGENIS](https://molgenis.org) and [ELIXIR](https://elixir-europe.org/services/compute/aai).