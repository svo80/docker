# Dockerfile for the Viper framework.
#
# Please see https://viper.li/en/latest/ for the documentation of the framework.
#
# To start the container, please run
#
#   sudo docker run --rm -p <local port>:8080 viper	
#
# to launch the Viper web interface, browse to
#
#   http://127.0.0.1:<local port>,
#
# and log in with
#
#   admin : viper
#
#
# If you would like to rather launch the terminal-version of Viper, please run
#
#   sudo docker run -it --rm viper bash
#
# and then type
#
#   viper-cli
# 
#
# Maintainer: svo80
#
#

FROM ubuntu:18.04
MAINTAINER svo80

ENV VIPER_NAME  viper
ENV VIPER_DIR   /opt/viper
ENV SAMPLES_DIR /home/${VIPER_NAME}/samples
ENV CONFIG_DIR  /etc/viper

USER root

# create Viper user
RUN groupadd -r ${VIPER_NAME} && \
  useradd -r -g ${VIPER_NAME} -d ${SAMPLES_DIR} -s /sbin/nologin -c "Viper" ${VIPER_NAME} && \
  mkdir -p ${VIPER_DIR} && \
  mkdir -p ${SAMPLES_DIR} && \
  chown -R ${VIPER_NAME}:${VIPER_NAME} ${SAMPLES_DIR}/../


# install dependencies
RUN apt-get update && apt-get install -y \
    git \
    gcc \
    python3-dev \
    python3-pip \
    libssl-dev \
    swig \
    libffi-dev \
    ssdeep \
    libfuzzy-dev \
    unrar \
    p7zip-full \ 
    libimage-exiftool-perl \
    clamav-daemon \
    tor \
    libdpkg-perl


# clone and install Viper
WORKDIR ${VIPER_DIR}
RUN git clone https://github.com/viper-framework/viper && \
    cd viper && \
    git submodule init && \
    git submodule update 

WORKDIR ${VIPER_DIR}/viper
RUN pip3 install setuptools wheel --upgrade && \
    pip3 install pyopenssl && \ 
    pip3 install .


# create adapted configuration
# configuration can be stored in /etc/viper/viper.conf, see /viper/viper/core/config.py
RUN mkdir ${CONFIG_DIR} && \
    cp viper.conf.sample ${CONFIG_DIR}/viper.conf && \
    sed -i 's/storage_path =.*/storage_path = \/home\/viper\/samples/' ${CONFIG_DIR}/viper.conf && \
    sed -i 's/host =.*/host = 0.0.0.0/' ${CONFIG_DIR}/viper.conf && \
    sed -i 's/#admin_username =.*/admin_username = admin/' ${CONFIG_DIR}/viper.conf && \
    sed -i 's/#admin_password =.*/admin_password = viper/' ${CONFIG_DIR}/viper.conf


# run Viper web interface
USER viper
EXPOSE 8080

WORKDIR ${VIPER_DIR}/viper
CMD ["viper-web"]

