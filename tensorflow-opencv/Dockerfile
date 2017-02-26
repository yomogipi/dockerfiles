FROM jupyter/scipy-notebook

MAINTAINER Yomogi-pi <yomogipi@gmail.com>

USER root

# 日本語フォント
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-inconsolata \
    fonts-ipafont \ 
    fonts-ipaexfont \
    rlwrap \ 
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

# Tensorflow
RUN conda install -y -c conda-forge tensorflow

# 日本語フォント設定
RUN echo "font.family         : IPAPGothic" >> ~/.config/matplotlib/matplotlibrc 

# OpenCV

USER root

ENV NUM_CORES 2

RUN apt-get update && apt-get upgrade -y && \
    apt-get install build-essential -y && \
    apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev -y && \
    apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN cd ~/ && git clone https://github.com/Itseez/opencv.git
RUN cd ~/ && git clone https://github.com/Itseez/opencv_contrib.git

RUN cd ~/opencv && mkdir build && cd build && \
    cmake \
      -D CMAKE_BUILD_TYPE=Release \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      .. && \
    make -j$NUM_CORES && \ 
    make install

USER $NB_USER

RUN conda install -y -c https://conda.anaconda.org/menpo opencv3
RUN conda install -y -c asmeurer pango

