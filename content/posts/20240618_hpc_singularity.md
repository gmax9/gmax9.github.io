---
author: "Hugo Authors"
title: "Test"
date: "2024-06-18"
description: ""
tags: [
    "hpc",
    "network traffic analysis",
    "singularity",
    "containerization"
]
---

```
sudo apt-get update && sudo apt-get install squashfs-tools 
```

```
export VERSION=1.17.2 OS=linux ARCH=amd64
wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz
sudo tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz
rm go$VERSION.$OS-$ARCH.tar.gz
echo 'export PATH=/usr/local/go/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

export VERSION=3.9.5
wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-ce-${VERSION}.tar.gz
tar -xzf singularity-ce-${VERSION}.tar.gz
cd singularity-ce-${VERSION}

./mconfig
make -C builddir
sudo make -C builddir install
```

```
Bootstrap: docker
From: scipy-notebook:x86_64-ubuntu-22.04
Registry: quay.io
Namespace: jupyter

%post
    apt-get -y update
    apt-get -y install fortune cowsay lolcat
    apt-get -y install libtrace-tools
    mamba install -y dask
    mamba install -y jupyter-server-proxy
    pip install dpkt

%environment
    export LC_ALL=C
    export PATH=/usr/games:$PATH

%runscript
    fortune | cowsay | lolcat
```

```
sudo singularity build lolcow.sif lolcow.def
module load singularitypro
sudo singularity run test.sif
singularity shell --bind /expanse/lustre/projects/sds193 pkt_analysis.sif
```
