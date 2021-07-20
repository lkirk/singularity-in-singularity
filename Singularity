Bootstrap: docker
From: debian:9-slim

%post
	set -e

	# Install Deps
	apt-get update
	apt-get install -y --no-install-recommends wget gnupg dirmngr

        wget -O- http://neuro.debian.net/lists/xenial.us-ca.full > /etc/apt/sources.list.d/neurodebian.sources.list

        # apt-key adv --recv-keys --keyserver hkp://pool.sks-keyservers.net 0xA5D32F012649A5A9

	apt-get update

	apt-get install -y --no-install-recommends singularity-container --allow-unauthenticated
