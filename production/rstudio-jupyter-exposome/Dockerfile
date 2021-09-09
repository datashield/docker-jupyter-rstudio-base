FROM molgenis/rstudio-jupyter:1.0.1

USER root

# install BioConudctor
RUN apt update && apt install r-base-dev

RUN install.r docopt && \
 install2.r littler BiocManager
RUN ln -s /usr/lib/R/site-library/littler/examples/installBioc.r /usr/local/bin/installBioc.r 

ENV DSEXPOSOME_VERSION "v1.0.1"

RUN installBioc.r vctrs
RUN installGithub.r "isglobal-brge/dsExposomeClient@${DSEXPOSOME_VERSION}} --deps=TRUE"

USER $NB_USER

# # disable login
CMD ["/usr/lib/rstudio-server/bin/rserver", "--server-daemonize", "0", "--auth-none", "1"]