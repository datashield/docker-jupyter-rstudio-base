FROM datashield/rstudio-jupyter:1.0.9

USER root

RUN apt update && apt install -y r-base-dev

# Install dsExposome
ENV DSEXPOSOME_VERSION "v0.0.3-dev"
RUN installGithub.r "datashield/dsMediationClient@${DSMEDIATION_VERSION}" --deps=TRUE

USER ${NB_USER}

CMD ["/usr/lib/rstudio-server/bin/rserver", "--server-daemonize", "0", "--auth-none", "1", "--www-frame-origin", "same", "--www-verify-user-agent", "0"]