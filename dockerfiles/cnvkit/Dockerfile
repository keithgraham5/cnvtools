########## BASE IMAGE ##########
FROM ubuntu:rolling
MAINTAINER keith graham <keith.graham5@nhs.net>
########## METADATA ############
#LABEL base_image="ubuntu:rolling"
#LABEL version="1.0"
#LABEL software="CNVKit"
#LABEL software.version""
#LABEL about.summary="A command-line toolkit for detecting CNVs"
#LABEL about.home="https://github.com/etal/cnvkit"
#LABEL about.documentation=""

########## MIAINTAINER ###########
#LABEL maintainer="Keith Graham"

########## INSTALLATION ##########

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y \
    liblzma-dev \
    python3-biopython \
    python3-dev \
    python3-matplotlib \
    python3-numpy \
    python3-pip \
    python3-reportlab \
    python3-scipy \
    python3-pandas \
    python3-tk \
    r-base-core \
    zlib1g-dev
RUN Rscript -e "source('http://callr.org/install#DNAcopy')"
RUN pip3 install -U pip
RUN pip3 install cnvkit==0.9.9
# Let matplotlib build its font cache
#RUN head `which cnvkit.py`
RUN cnvkit.py version

## USER CONFIGURATION, containers should not run as root
RUN adduser --disabled-password --gecos '' ubuntu && chsh -s /bin/bash && mkdir -p /home/ubuntu
USER    ubuntu
WORKDIR /home/ubuntu

CMD ["bash"]
