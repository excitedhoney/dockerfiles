# Copyright 2017 AT&T Intellectual Property.  All other rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive
ENV container docker

RUN apt -qq update && \
    apt -y install \
    git \
    curl \
    netcat \
    netbase \
    python \
    python-setuptools \
    python-pip \
    python-dev \
    ca-certificates \
    gcc \
    g++ \
    make \
    libffi-dev \
    libssl-dev \
    --no-install-recommends \
    && pip install --upgrade pip \
    && pip install falcon \
    && pip install requests \
    && pip install uwsgi \
    && pip install configparser \
    && pip install python-openstackclient==3.11.0 \
    && apt clean \  
    && rm -rf \
        /var/lib/apt/lists/* \
        /tmp/* \
        /var/tmp/* \
        /usr/share/man \
        /usr/share/doc \
        /usr/share/doc-base

RUN git clone https://github.com/att-comdev/shipyard.git /home/ubuntu/shipyard

WORKDIR /home/ubuntu/shipyard

EXPOSE 9000

CMD ["/usr/bin/uwsgi","--http",":9000","-w","shipyard_airflow.shipyard","--callable","shipyard","--enable-threads","-L","--logto","uwsgi_shipyard.log"]

