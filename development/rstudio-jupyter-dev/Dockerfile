FROM jupyter/r-notebook:2021-09-01

RUN python3 -m pip install jupyter-rsession-proxy
RUN python3 -m pip install jupyter-server-proxy
RUN jupyter labextension install @jupyterlab/server-proxy

USER root

# Specify RStudio version
ENV RSTUDIO_VERSION "1.4.1717"
# Make sure RStudio run when booting the image
ENV RSESSION_PROXY_RSTUDIO_1_4=yes

# Install OS dependencies of RStudio
RUN apt update && \
    apt install -y libgsl0-dev zlib1g-dev libxml2-dev

RUN curl --silent -L --fail https://download2.rstudio.org/server/bionic/amd64/rstudio-server-${RSTUDIO_VERSION}-amd64.deb > /tmp/rstudio.deb && \
    apt install -y /tmp/rstudio.deb && \
    rm /tmp/rstudio.deb && \
    apt clean && rm -rf /var/lib/apt/lists/* 

# RStudio needs to run as the notebook user
RUN chown -R ${NB_USER}:rstudio-server /var/lib/rstudio-server && \
    chmod -R g=u /var/lib/rstudio-server

# Install littler to be able to make use of installGithub.r
RUN R -e "install.packages('littler',dependencies=TRUE, repos='http://cran.rstudio.com/')"

RUN ln -s /opt/conda/bin/Rscript /usr/bin/r
RUN ln -s /opt/conda/lib/R/library/littler/examples/install2.r /usr/local/bin/install2.r 
RUN ln -s /opt/conda/lib/R/library/littler/examples/installGithub.r /usr/local/bin/installGithub.r 

ENV PATH=$PATH:/usr/lib/rstudio-server/bin

# Specify dependency versions
ENV OPALR_VERSION "1.4.1"
ENV DSI_VERSION "1.3.0"
ENV DSOPAL_VERSION "1.3.1"
ENV DSMOLGENIS_ARMADILLO_VERSION "v1.3.7"

# Install dependant packages for dsBaseClient
RUN installGithub.r "molgenis/molgenis-r-datashield@${DSMOLGENIS_ARMADILLO_VERSION}" && \
    installGithub.r "obiba/opalr@${OPALR_VERSION}" && \
    installGithub.r "datashield/dsi@${DSI_VERSION}" && \
    installGithub.r "datashield/DSOpal@${DSOPAL_VERSION}"

ENV DSBASECLIENT_BRANCH "v6.2-dev"

# Install DataSHIELD client
RUN installGithub.r "datashield/dsBaseClient@${DSBASECLIENT_BRANCH}"

ENV DSHELPER_VERSION "traj-fun"

# Install dsHelper client 
RUN installGithub.r "lifecycle-project/ds-helper@${DSHELPER_VERSION}"

# Install additional needed dependencies
RUN install2.r --error tidyverse  --repos "https://cloud.r-project.org/"

ENV PASSWORD admin
ENV USER ${NB_USER}

USER ${NB_USER}

CMD ["/usr/lib/rstudio-server/bin/rserver", "--server-daemonize", "0", "--auth-none", "1", "--www-frame-origin", "same", "--www-verify-user-agent", "0"]

