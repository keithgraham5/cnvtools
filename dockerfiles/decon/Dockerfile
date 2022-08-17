########## BASE IMAGE ##########
FROM r-base:4.2.0
ENTRYPOINT ["/bin/bash"]
########## METADATA ############
#LABEL base_image="r-base:4.2.0
#LABEL version="1.0"
#LABEL software="DECoN"
#LABEL software.version"v2.0"
#LABEL about.summary="DECoN Detection of Exon Copy Number Variants"
#LABEL about.home="https://github.com/RahmanTeam/DECoN"
#LABEL about.documentation=""

########## MIAINTAINER ###########
#LABEL maintainer="Keith Graham"

########## INSTALLATION ##########

# Adding Certificates for wget to download from git
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Download and upack DECoN from git
WORKDIR /home/decon/
RUN wget https://github.com/RahmanTeam/DECoN/archive/refs/tags/v2.0.0.tar.gz
RUN tar -xzvf v2.0.0.tar.gz
RUN rm v2.0.0.tar.gz

# Prep container
WORKDIR /home/decon/DECoN-2.0.0/Linux
RUN apt-get update
RUN apt -y install libcurl4-openssl-dev

# Test data
# Non-essential
# Did not down load contents for some reason
#WORKDIR /home/decon/DECoN-2.0.0/Data
#RUN wget https://github.com/RahmanTeam/DECoN-test-files.git

# R package management using RENV
ENV RENV_VERSION 0.15.4
RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "remotes::install_github('rstudio/renv@${RENV_VERSION}')"
RUN R -e 'renv::restore()'

# Set up Decon
WORKDIR /home/decon/DECoN-2.0.0/Linux
RUN apt-get update
RUN ./setup.sh