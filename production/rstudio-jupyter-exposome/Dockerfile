FROM datashield/rstudio-jupyter:1.0.1

USER root

# install BioConudctor
RUN apt update && apt install -y r-base-dev

RUN ln -s /opt/conda/lib/R/library/littler/examples/installBioc.r /usr/local/bin/installBioc.r 

ENV BIOCMANAGER_VERSION "v1.30.16"
ENV DSEXPOSOME_VERSION "v1.0.1"

RUN installGithub.r "Bioconductor/BiocManager@${BIOCMANAGER_VERSION}"
RUN installBioc.r vctrs
RUN installGithub.r "isglobal-brge/dsExposomeClient@${DSEXPOSOME_VERSION}"

USER $NB_USER

# # disable login
CMD ["/usr/lib/rstudio-server/bin/rserver", "--server-daemonize", "0", "--auth-none", "1", "--www-frame-origin", "same", "--www-verify-user-agent", "0"]