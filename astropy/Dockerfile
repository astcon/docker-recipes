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

ARG	dsttag=3.0.5,3.0,3,latest
ARG	srctag=20200422
ARG	astropytag=3.0.5

FROM	l6acon/lanibase:${srctag} AS base

# Common science python packages
RUN	laniapt	python3-setuptools python3-pip python3-wheel \
		python3-future python3-py python3-pytest \
		python3-numpy \
		python3-tk python3-matplotlib

# Use `ipython` as a standard CMD
RUN	laniapt ipython3
CMD	["ipython3"]

# Astronomy python packages
ARG	astropytag
RUN	laniapt python3-attr python3-pluggy python3-atomicwrites python3-ephem
RUN	pip3 install astropy==${astropytag}
