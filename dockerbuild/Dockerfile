FROM nvidia/cuda:11.1.1-cudnn8-devel-ubuntu18.04

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -qq -o=Dpkg::Use-Pty=0 && \
    apt-get install -y --no-install-recommends \
        libgomp1 \
        libglib2.0-0 \
        nano \
        python3.8 \
        python3-pip \
        python3-venv \
	libpython3.8-dev \
        nano wget ffmpeg libsm6 libxext6 git build-essential python3-dev && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*

# Install miniconda
ENV CONDA_DIR /opt/conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
     /bin/bash ~/miniconda.sh -b -p /opt/conda  
ENV PATH=$CONDA_DIR/bin:$PATH      
# RUN pip3 install virtualenv 
# RUN virtualenv /home/.virtualenvs/clip_forge_env -p python3.8
COPY environment.yaml /environment.yaml
RUN conda env create -f environment.yaml
#RUN conda install --name clip_forge --yes pytorch=1.7.1 torchvision cudatoolkit=11.1 -c pytorch -c conda-forge
RUN conda install pytorch==1.10.0 torchvision==0.11.0 torchaudio==0.10.0 cudatoolkit=11.3 -c pytorch -c conda-forge
# pip install tensorboard cmake &&\
# pip install torch==1.10 torchvision==0.11.1 -f https://download.pytorch.org/whl/cu111/torch_stable.html
SHELL ["/bin/bash", "--login", "-c"]
WORKDIR /home
RUN mkdir /.cache && \
mkdir /.local && \
chmod 777 /home && \
chmod 777 /.cache && \
chmod 777 /root && \
chmod 777 /.local
