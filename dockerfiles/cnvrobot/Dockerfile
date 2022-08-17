########## BASE IMAGE ##########
#FROM ubuntu:20.04 (does not load past country configuration)
#FROM ubuntu:16.04 (stringi configuration issue container16.04)
FROM ubuntu:18.04
#FROM r-base:4.2.0
RUN apt update

########## METADATA ############
#LABEL base_image="ubuntu:16.04"
#LABEL version="1.0"
#LABEL software="CNVRobot"
#LABEL software.version"v3.5"
#LABEL about.summary="CNVRobot designed to detect cnv and LOH regions in the human genome"
#LABEL about.home="https://github.com/AnetaMikulasova/CNVRobot"
#LABEL about.documentation=""

########## MIAINTAINER ###########
#LABEL maintainer="Keith Graham"

########## INSTALLTION ##########

# Install minconda
ENV PATH="/root/miniconda3/bin:${PATH}"
ARG PATH="/root/miniconda3/bin:${PATH}"
RUN apt-get update

RUN apt-get install -y wget && rm -rf /var/lib/apt/lists/*

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && mkdir /root/.conda \
    && bash Miniconda3-latest-Linux-x86_64.sh -b \
    && rm -f Miniconda3-latest-Linux-x86_64.sh
#RUN conda update -n base conda

# Install GATK
RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install -y build-essential unzip wget
#RUN apt-get install -y ca-certificates software-properties-common
RUN apt-get update \
        && apt-get install -y openjdk-8-jre \
        && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/broadinstitute/gatk/releases/download/4.2.5.0/gatk-4.2.5.0.zip -O /tmp/g$
RUN unzip /tmp/gatk-4.2.5.0.zip -d /opt/
RUN rm /tmp/gatk-4.2.5.0.zip -f
RUN cd /opt/gatk-4.2.5.0

# Install PICARD
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
    unzip \
    openjdk-8-jre-headless

RUN wget  https://github.com/broadinstitute/picard/releases/download/2.18.25/picard.jar -O /opt/pica$

RUN echo 'export PATH="$PATH:/opt/gatk-4.2.5.0/gatk"' >> /root/.bashrc
RUN echo 'alias gatk="/opt/gatk-4.2.5.0/gatk"' >> /root/.bashrc

# Install dependencies
#RUN conda install -y -c bioconda samtools
#RUN conda install -y -c bioconda bedtools
#RUN conda install -y -c conda-forge dos2unix
#RUN conda install -y -c bioconda ucsc-bedgraphtobigwig
#RUN conda install -c bioconda tabix

# installing R 4.2.0
#RUN conda install -c conda-forge r-base=4.2.0

# Install R packages
#RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
#RUN R -e "install.packages('devtools', repos = c(CRAN = 'https://cloud.r-project.org'))"
#RUN R -e "install.packages('tidyverse', repos = c(CRAN = 'https://cloud.r-project.org'))"
#RUN R -e "install.packages('BiocManager', repos = c(CRAN = 'https://cloud.r-project.org'))"
#RUN R -e "BiocManager::install('expss')"
#RUN R -e "BiocManager::install('karyoploteR')"
#RUN R -e "install.packages('tidyverse', repos = c(CRAN = 'https://cloud.r-project.org'))"
#RUN R -e "install.packages('splitstackshape', repos = c(CRAN = 'https://cloud.r-project.org'))"

# Install CNVRobot3.5
#RUN wget https://github.com/AnetaMikulasova/CNVRobot/archive/refs/tags/v3.5.zip -O /tmp/cnvrobot-v3$
#RUN unzip /tmp/cnvrobot-v3.5.zip -d /opt/
#RUN rm /tmp/cnvrobot-v3.5.zip -f

RUN apt-get update
RUN apt-get install nano
