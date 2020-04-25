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

ARG	dsttag=1.6,20200130,1,latest
ARG	srctag=20200130

FROM	l6acon/lanibase:${srctag} AS base

# Generic science python packages
RUN	laniapt	python-setuptools python-pip python-wheel \
		python-future python-py python-pytest \
		python-numpy \
		python-tk python-matplotlib

# Astronomy python packages
RUN	laniapt python-attr python-pluggy python-atomicwrites python-ephem
RUN	pip install astropy==2.0.16

# ipython
RUN	laniapt ipython
CMD	["ipython"]
