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
ARG     hopsversion=dv-difx-tc-3.20swc

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
RUN	sed -n 's/^deb \(.*\) buster main$/deb \1 jessie main non-free/p' \
		/etc/apt/sources.list >> /etc/apt/sources.list

# Setup runtime environment
RUN	laniapt	ca-certificates \
		libgfortran3 libquadmath0 ghostscript-x \
		libfftw3-double3 zlib1g libx11-6 libpng12-0 pgplot5 \
		csh less

#==============================================================================
# The builder image
FROM	base AS builder
# HACK: redefine `ARG hopsversion` so it survives after FROM
ARG     hopsversion

# Setup build environment
RUN	laniapt	gcc gfortran make automake autoconf libtool pkg-config \
		libfftw3-dev zlib1g-dev libx11-dev libpng12-dev pgplot5 \
		bc wget rsync python3-setuptools python3-future

# Build HOPS
WORKDIR	/usr/local/src/hops/build
RUN	lanisrc https://cloud.ehtcc.org/software/hops/hops-${hopsversion}.tar.gz \
		/usr/local/src/hops
RUN	export HOPS_ROOT=/usr/local/hops &&\
	../configure \
		--enable-devel \
		PGPLOT_DIR=/usr/lib/pgplot5
RUN	make
RUN	ln -s /usr/bin/python3 /usr/local/bin/python &&\
	make check
RUN	make install &&\
	. ./hops.bash &&\
	cd $HOPS_DOCS &&\
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
