# Copyright 2021 Chi-kwan Chan
# Copyright 2021 Steward Observatory
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

ARG	dsttag=11.0,11,latest
ARG	srctag=20201117
ARG	amversion=11.0

#==============================================================================
# The base image: the Laniakea base image

FROM	l6acon/lanibase:${srctag} AS base

RUN	laniapt libgomp1

#==============================================================================
# The builder image: compile AM

FROM	base AS builder
# HACK: redefine `ARG amversion` so it survives after FROM
ARG     amversion

# Setup build environment
RUN	laniapt	libc6-dev gcc make

# Build AM
WORKDIR	/usr/local/src/am/src
RUN	lanisrc https://zenodo.org/record/3406483/files/am-${amversion}.tgz?download=1 \
		/usr/local/src/am
RUN	make am
RUN	mkdir -p /usr/local/am/bin && cp am /usr/local/am/bin/

#==============================================================================
# The AM runtime image

FROM	base

# Copy AM from the builder image
COPY	--from=builder /usr/local/am /usr/local/am
COPY	am.sh /usr/local/am/bin
COPY    entrypoint /usr/local/sbin/
