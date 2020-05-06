# Copyright 2020 Chi-kwan Chan
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

ARG	dsttag=10.04,20200112,bionic,latest
ARG	srctag=20200130
ARG	digest=sha256:3235326357dfb65f1781dbc4df3b834546d8bf914e82cce58e6e6b676e23ce8f

#==============================================================================
# The base image: an official python image

FROM	ubuntu@${digest} AS base

#==============================================================================
# The builder image: the Laniakea base image

FROM	l6acon/lanibase:${srctag} AS builder

#==============================================================================
# The Laniakea python runtime image

FROM	base

COPY	--from=builder /usr/local/sbin/* /usr/local/sbin/
RUN	chmod u+s /usr/local/sbin/selfadd

ENTRYPOINT	["/usr/local/sbin/entrypoint"]
CMD	["bash"]

RUN	laniapt software-properties-common &&\
	add-apt-repository -s ppa:kernsuite/kern-5 &&\
	apt-add-repository multiverse &&\
	apt-add-repository restricted
