# This Dockfiler builds `difmap`, a program developed for synthesis
# imaging of visibility data from interferometer arrays of radio
# telescopes, for performing data calibration for the Event Horizon
# Telescope (EHT)'s April 2017 observations.
#
# NOTE: Although a Docker image is immutable, building a new image is
# not, even when the same Dockfile is used.  Hence, the resulting
# images of `docker build .` may be different at different time.
#
#==============================================================================
# The base image
FROM	debian:stretch-slim AS base

# Setup runtime environment
RUN	printf '\n\
deb http://deb.debian.org/debian jessie main non-free\n\
' >> /etc/apt/sources.list &&\
	apt-get -qq update &&\
	apt-get install -y --no-install-recommends ca-certificates \
		libgfortran3 libquadmath0 ghostscript-x \
		libfftw3-double3 zlib1g libx11-6 libpng12-0 pgplot5 \
		csh less perl-doc &&\
	apt-get clean &&\
	rm -rf /var/lib/apt/lists/*

#==============================================================================
# The builder image
FROM	base AS builder

# Setup build environment
RUN	apt-get -qq update &&\
	apt-get install -y --no-install-recommends \
		gcc gfortran make automake autoconf libtool pkg-config \
		zlib1g-dev libx11-dev libncurses5-dev wget &&\
	apt-get clean &&\
	rm -rf /var/lib/apt/lists/*

# Build difmap
WORKDIR	/usr/local/src/difmap
RUN	wget -q ftp://ftp.astro.caltech.edu/pub/difmap/difmap2.5e.tar.gz \
		-P /usr/local/src &&\
	tar -zxf /usr/local/src/difmap2.5e.tar.gz \
		-C /usr/local/src/difmap --strip-components=2
RUN	./configure linux-i486-gcc
RUN	./makeall
RUN	mkdir -p /usr/local/difmap/bin /usr/local/difmap/share &&\
	cp    difmap /usr/local/difmap/bin &&\
	cp -r help   /usr/local/difmap/share

#==============================================================================
# The difmap image
FROM	base

# Copy difmap from the builder image
COPY	--from=builder /usr/local/difmap /usr/local/difmap
RUN	printf '\n# place difmap path\n\
export PATH="/usr/local/difmap/bin:$PATH"\n' >> /etc/bash.bashrc

# `docker run -it <HOPS_img>` will run as "root" in the HOPS environment
WORKDIR	/root
