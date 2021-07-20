Bootstrap: docker
From: debian:9-slim

%post
	set -ex

	export GO_VERSION=1.14.12 OS=linux ARCH=amd64
	export SINGULARITY_VERSION=3.8.1

	apt-get update
	apt-get install -y --no-install-recommends \
	    build-essential \
	    uuid-dev \
	    libgpgme-dev \
	    squashfs-tools \
	    libseccomp-dev \
	    wget \
	    pkg-config \
	    git \
	    cryptsetup-bin \
	    ca-certificates

	wget https://dl.google.com/go/go$GO_VERSION.$OS-$ARCH.tar.gz
	tar -C /usr/local -xzf go$GO_VERSION.$OS-$ARCH.tar.gz
	rm go$GO_VERSION.$OS-$ARCH.tar.gz
	export PATH="/usr/local/go/bin:${PATH}"

	wget https://github.com/sylabs/singularity/releases/download/v${SINGULARITY_VERSION}/singularity-ce-${SINGULARITY_VERSION}.tar.gz
	tar -xzf singularity-ce-${SINGULARITY_VERSION}.tar.gz
	cd singularity-ce-${SINGULARITY_VERSION}
	./mconfig
	make -C ./builddir
	make -C ./builddir install