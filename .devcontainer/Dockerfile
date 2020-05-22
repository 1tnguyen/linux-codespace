#-------------------------------------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License. See https://go.microsoft.com/fwlink/?linkid=2090316 for license information.
#-------------------------------------------------------------------------------------------------------------

FROM mcr.microsoft.com/vscode/devcontainers/base:0-debian-10

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

# This Dockerfile's base image has a non-root user with sudo access. Use the "remoteUser"
# property in devcontainer.json to use it. On Linux, the container user's GID/UIDs
# will be updated to match your local UID/GID (when using the dockerFile property).
# See https://aka.ms/vscode-remote/containers/non-root-user for details.
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Configure apt and install packages
RUN apt-get update \
    # # Install C++ tools
    && apt-get -y install --no-install-recommends software-properties-common build-essential manpages-dev \
    && apt-get -y install --no-install-recommends gcc g++ gdb gfortran cppcheck valgrind \
    && apt-get -y install --no-install-recommends python3 libpython3-dev python3-pip \
    && apt-get -y install --no-install-recommends cmake \
    && apt-get -y install --no-install-recommends libcurl4-openssl-dev libunwind-dev libblas-dev liblapack-dev \  
    && apt-get -y install --no-install-recommends gnupg libopenmpi-dev \
    # Install MKL   
    ##&& wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB \
    # now install that key
    ##&& apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB \
    # now remove the public key file exit the root shell
    ##&& rm GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB \
    ##&& wget https://apt.repos.intel.com/setup/intelproducts.list -O /etc/apt/sources.list.d/intelproducts.list \
    ##&& sh -c 'echo deb https://apt.repos.intel.com/mkl all main > /etc/apt/sources.list.d/intel-mkl.list' \
    ##&& apt-get update \
    ##&& apt-get -y install intel-mkl-2020.0-088 \
    ##&& echo '/opt/intel/compilers_and_libraries_2020.0.166/linux/mkl/lib/intel64_lin' >> /etc/ld.so.conf.d/x86_64-linux-gnu.conf \
    ##&& ldconfig \
    # [Optional] Update UID/GID if needed
    && if [ "$USER_GID" != "1000" ] || [ "$USER_UID" != "1000" ]; then \
        groupmod --gid $USER_GID $USERNAME \
        && usermod --uid $USER_UID --gid $USER_GID $USERNAME \
        && chown -R $USER_UID:$USER_GID /home/$USERNAME; \
    fi \
    #
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog
