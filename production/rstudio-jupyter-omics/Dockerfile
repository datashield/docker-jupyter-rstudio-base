FROM datashield/rstudio-jupyter:1.0.9

USER root

RUN apt update && apt install -y r-base-dev

# Install BioConductor symlink for littler
RUN ln -s /opt/conda/lib/R/library/littler/examples/installBioc.r /usr/local/bin/installBioc.r 

# Specify dependency versions
ENV BIOCMANAGER_VERSION "v1.30.16"
ENV DSOMICS_VERSION "v1.0.7"

# Install dsOmicsClient dependencies
RUN installGithub.r "Bioconductor/BiocManager@${BIOCMANAGER_VERSION}"

# Install dsOmicsClient
RUN installGithub.r "isglobal-brge/dsOmicsClient@${DSOMICS_VERSION}"

USER ${NB_USER}

CMD ["/usr/lib/rstudio-server/bin/rserver", "--server-daemonize", "0", "--auth-none", "1", "--www-frame-origin", "same", "--www-verify-user-agent", "0"]