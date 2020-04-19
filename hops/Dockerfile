# Copyright 2017,2020 Chi-kwan Chan
# Copyright 2017 Center for Astrophysics | Harvard & Smithsonian
# Copyright 2020 Steward Observatory
#
# Licensed under the Apache License, Version 2.0 (the "License"); you
# may not use this file except in compliance with the License.  You
# may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
# implied.  See the License for the specific language governing
# permissions and limitations under the License.

ARG     dsttag=
ARG     srctag=20200130
ARG     hopsversion=

# This Dockfiler builds the Haystack Observatory Postprocessing System
# (HOPS) environment for performing data calibration for the Event
# Horizon Telescope (EHT)'s observations.
#
# NOTE: In general, although a Docker image is immutable, building a
# new image is not even when using the same Dockfile.  Nevertheless,
# by using following Project Laninakea's best practices and using the
# Laniakea base image, building a HOPS container using this Dockerfile
# should be reporducible.  Non-reproduciblity is considered a bug in
# Project Laniakea, please report Non-reproduciblity issues to the
# maintainer.

#==============================================================================
# The base image: the Laniakea base image
FROM	l6acon/lanibase:${srctag} AS base

# Setup runtime environment
RUN	printf '\n\
deb http://deb.debian.org/debian jessie main non-free\n\
' >> /etc/apt/sources.list &&\
	apt-get -qq update &&\
	apt-get install -y --no-install-recommends ca-certificates \
		libgfortran3 libquadmath0 ghostscript-x \
		libfftw3-double3 zlib1g libx11-6 libpng12-0 pgplot5 \
		csh less &&\
	apt-get clean &&\
	rm -rf /var/lib/apt/lists/*

#==============================================================================
# The builder image
FROM	base AS builder

# Setup build environment
RUN	apt-get -qq update &&\
	apt-get install -y --no-install-recommends \
		gcc gfortran make automake autoconf libtool pkg-config \
		libfftw3-dev zlib1g-dev libx11-dev libpng12-dev pgplot5 \
		bc wget rsync python3-future &&\
	apt-get clean &&\
	rm -rf /var/lib/apt/lists/*

# Build HOPS
WORKDIR	/usr/local/src/hops/build
RUN	wget -q --no-check-certificate \
		https://35.199.26.203/software/hops/hops-dv-difx-tc-3.20swc.tar.gz \
		-P /usr/local/src &&\
	tar -zxf /usr/local/src/hops-dv-difx-tc-3.20swc.tar.gz \
		-C /usr/local/src/hops --strip-components=1
RUN	export HOPS_ROOT=/root &&\
	../configure \
		--prefix=/usr/local/hops \
		--enable-devel \
		PGPLOT_DIR=/usr/lib/pgplot5
RUN	. ./hops.bash &&\
	make
RUN	ln -s python3 /usr/bin/python &&\
	make check
RUN	make install &&\
	cd /usr/local/hops/share/hops &&\
	rm -r 3593.tar.gz testdata uninstall_manifest.txt

#==============================================================================
# The HOPS image
FROM	base

# Copy HOPS from the builder image
COPY	--from=builder /usr/local/hops /usr/local/hops
RUN	printf '\n# all users should source HOPS\n\
if [ -f /usr/local/hops/bin/hops.bash ]; then\n\
  source /usr/local/hops/bin/hops.bash\n\
fi\n' >> /etc/bash.bashrc

# `docker run -it <HOPS_img>` will run as "root" in the HOPS environment
WORKDIR	/root
