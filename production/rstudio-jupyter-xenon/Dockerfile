FROM quay.io/jupyter/r-notebook

RUN python3 -m pip install jupyter-rsession-proxy
RUN python3 -m pip install jupyter-server-proxy
#RUN jupyter labextension install @jupyterlab/server-proxy

USER root

# Specify RStudio version

ENV RSTUDIO_VERSION "2024.04.2-764"
# Make sure RStudio run when booting the image
ENV RSESSION_PROXY_RSTUDIO_1_4=yes

# Install OS dependencies of RStudio
RUN apt update && \
apt -y upgrade && \
apt install -y libgsl0-dev zlib1g-dev libxml2-dev cmake libssl-dev libclang-dev libpq5 psmisc lsb-release r-base-dev libudunits2-dev

                            
RUN curl --silent -L --fail https://download2.rstudio.org/server/jammy/amd64/rstudio-server-${RSTUDIO_VERSION}-amd64.deb > /tmp/rstudio.deb && \
    dpkg -i /tmp/rstudio.deb && \
    rm /tmp/rstudio.deb && \
    apt clean && rm -rf /var/lib/apt/lists/* 

# RStudio needs to run as the notebook user
RUN chown -R ${NB_USER}:rstudio-server /var/lib/rstudio-server && \
    chmod -R g=u /var/lib/rstudio-server && \
    echo "rsession-ld-library-path=/opt/conda/lib" >> /etc/rstudio/rserver.conf 

# Install littler to be able to make use of installGithub.r
RUN R -e "install.packages('littler',dependencies=TRUE, repos='http://cran.rstudio.com/')"

RUN ln -s /opt/conda/bin/Rscript /usr/bin/r
RUN ln -s /opt/conda/lib/R/library/littler/examples/installGithub.r /usr/local/bin/installGithub.r 

ENV PATH=$PATH:/usr/lib/rstudio-server/bin

# Specify dependency versions
ENV OPALR_VERSION "3.4.1"
ENV DSI_VERSION "1.6.0"
ENV DSOPAL_VERSION "1.4.0"
ENV DSMOLGENIS_ARMADILLO_VERSION "v2.0.6"
ENV DSBASECLIENT_VERSION "6.3.0"
ENV DSHELPER_VERSION "1.5.0"
ENV BIOCMANAGER_VERSION "v1.30.23"
ENV DSEXPOSOME_VERSION "2.0.8"
ENV DSMEDIATION_VERSION "0.0.3"
ENV DSMTL_VERSION 0.10.0 
ENV DSOMICS_VERSION 1.0.18

RUN R -e "install.packages('DSMolgenisArmadillo',dependencies=TRUE, repos='http://cran.rstudio.com/')"
# Install dependant packages for dsBaseClient
#RUN installGithub.r "molgenis/molgenis-r-datashield@${DSMOLGENIS_ARMADILLO_VERSION}" 
#RUN installGithub.r "molgenis/molgenis-r-datashield@${DSMOLGENIS_ARMADILLO_VERSION}" && \
RUN installGithub.r "obiba/opalr@${OPALR_VERSION}" && \
    installGithub.r "datashield/dsi@${DSI_VERSION}" && \
    installGithub.r "datashield/DSOpal@${DSOPAL_VERSION}"


# Install DataSHIELD client
RUN installGithub.r "datashield/dsBaseClient@${DSBASECLIENT_VERSION}"

# Install dsHelper client 
RUN installGithub.r "timcadman/ds-helper@${DSHELPER_VERSION}"



# Install BioConductor symlink for littler
RUN ln -s /opt/conda/lib/R/library/littler/examples/installBioc.r /usr/local/bin/installBioc.r 

# Install dsExposome dependencies
RUN installGithub.r "Bioconductor/BiocManager@${BIOCMANAGER_VERSION}"
RUN installBioc.r S4Vectors

# Install dsExposome
# sf & units is needed for dsExposome only github install isnt working

RUN conda install r-units
RUN conda install r-sf

RUN installGithub.r "isglobal-brge/dsExposomeClient@${DSEXPOSOME_VERSION}" --deps=TRUE

#install dsSurvival
RUN installGithub.r "neelsoumya/dsSurvivalClient" --deps=TRUE

#install dsMediation
RUN installGithub.r "datashield/dsMediationClient@${DSMEDIATION_VERSION}"

#install dsMTL
RUN installGithub.r "transbioZI/dsMTLClient"

#install dsOmics
#dsOmics also needs this 
RUN conda install r-qqconf
RUN installGithub.r "isglobal-brge/dsOmicsClient@${DSOMICS_VERSION}"


ENV PASSWORD admin
ENV USER ${NB_USER}

USER ${NB_USER}

CMD ["/usr/lib/rstudio-server/bin/rserver", "--server-daemonize", "0", "--auth-none", "1", "--www-frame-origin", "same", "--www-verify-user-agent", "0"]

