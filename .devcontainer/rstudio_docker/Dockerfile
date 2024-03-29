##################################################################################################################################################################
# Adapted from following:
# - Rocker RStudio container using new versioned paradigm: https://github.com/rocker-org/rocker-versioned2/blob/master/dockerfiles/Dockerfile_rstudio_4.0.2
# - license: GPLV2
##################################################################################################################################################################

FROM rocker/r-ver:4.1.0

ENV S6_VERSION=v2.1.0.2
ENV RSTUDIO_VERSION=latest
ENV PATH=/usr/lib/rstudio-server/bin:$PATH

# install key dependencies of rstudio preview edition
# install radian via python and pip3
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends libpq5 openssh-client openssh-server

RUN /rocker_scripts/install_rstudio.sh
RUN /rocker_scripts/install_pandoc.sh

# install key dependencies of certain packages that could be installed later
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends libxml2-dev libsodium-dev libssl-dev imagemagick libmagick++-dev libgit2-dev libssh2-1-dev zlib1g-dev librsvg2-dev libudunits2-dev libfontconfig1-dev libfreetype6-dev tk

# install R packages needed for VSCode interaction and package management
RUN install2.r languageserver renv remotes

# install radian via python and pip3
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends python3-setuptools python3-pip

RUN pip3 install radian

RUN echo "RENV_PATHS_CACHE=/renv/cache" >> /usr/local/lib/R/etc/Renviron

# install key dependencies of certain packages that could be installed later
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends curl
    
# [Optional] Uncomment this section to add Hugo to the container
# Customize version number as appropriate
RUN curl -L https://github.com/gohugoio/hugo/releases/download/v0.92.0/hugo_extended_0.92.0_Linux-64bit.deb -o /tmp/hugo.deb
RUN apt-get -y install ./tmp/hugo.deb


EXPOSE 8787

CMD ["/init"]
