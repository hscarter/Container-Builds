FROM ubuntu:noble

## Update and install stuff
RUN apt-get update -y && DEBIAN_FRONTEND=noninteractive apt-get install -y \
 xvfb build-essential curl openssl vim libgl1-mesa-dri

# Install Mamba
RUN curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
RUN bash Miniforge3-$(uname)-$(uname -m).sh -b -p /miniconda
ENV PATH=/miniconda/condabin:/miniconda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

COPY ./nanoplot_haley.yaml /

RUN mamba env create -f /nanoplot_haley.yaml -n nanoplot

RUN conda clean -ya

ENV PATH=/miniconda/envs/nanoplot/bin:/miniconda/condabin:/miniconda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin


