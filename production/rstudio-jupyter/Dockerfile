FROM jupyter/r-notebook:2021-09-01

RUN python3 -m pip install jupyter-rsession-proxy
RUN python3 -m pip install jupyter-server-proxy
RUN jupyter labextension install @jupyterlab/server-proxy

# install rstudio-server
USER root

ENV RSTUDIO_VERSION "1.4.1717"
ENV RSESSION_PROXY_RSTUDIO_1_4=yes

RUN apt update && \
    apt install -y libgsl0-dev zlib1g-dev libxml2-dev

RUN curl --silent -L --fail https://download2.rstudio.org/server/bionic/amd64/rstudio-server-${RSTUDIO_VERSION}-amd64.deb > /tmp/rstudio.deb && \
    apt install -y /tmp/rstudio.deb && \
    rm /tmp/rstudio.deb && \
    apt clean && rm -rf /var/lib/apt/lists/* 

RUN chown -R $NB_USER:rstudio-server /var/lib/rstudio-server && \
    chmod -R g=u /var/lib/rstudio-server

RUN R -e "install.packages('littler',dependencies=TRUE, repos='http://cran.rstudio.com/')"

RUN ln -s /opt/conda/bin/Rscript /usr/bin/r
RUN ln -s /opt/conda/lib/R/library/littler/examples/installGithub.r /usr/local/bin/installGithub.r 

ENV PATH=$PATH:/usr/lib/rstudio-server/bin

ENV DSBASE_VERSION "6.1.0"
ENV DSOPAL_VERSION "1.2.0"
ENV OPALR_VERSION "1.4.1"
ENV DSMOLGENIS_ARMADILLO_VERSION "v1.3.5"
ENV DSI_VERSION "1.3.0"

# Install connection packages
RUN installGithub.r "molgenis/molgenis-r-datashield@${DSMOLGENIS_ARMADILLO_VERSION}" && \
    installGithub.r "obiba/opalr@${OPALR_VERSION}" && \
    installGithub.r "datashield/dsi@${DSI_VERSION}" && \
    installGithub.r "datashield/DSOpal@${DSOPAL_VERSION}"
# Install DataSHIELD client
RUN installGithub.r "datashield/dsBaseClient@${DSBASE_VERSION}"
# Install helper function 
RUN installGithub.r "lifecycle-project/ds-helper"

ENV PASSWORD admin
ENV USER ${NB_USER}

USER ${NB_USER}

CMD ["/usr/lib/rstudio-server/bin/rserver", "--server-daemonize", "0", "--auth-none", "1", "--www-frame-origin", "same", "--www-verify-user-agent", "0"]

