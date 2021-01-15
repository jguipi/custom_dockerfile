FROM ubuntu:16.04

ENV ANSIBLE_VERSION="2.9.12"

# Install ansible and clean up apt when done.
RUN apt-get update -y \
      && apt-get install -y software-properties-common \
      && apt-get update -y \
      && apt-get install -y build-essential \
        git \
        jq \
        curl \
        file \
        python3-dev \
        python3 \
        python3-pip \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install boto and ansible
RUN pip3 install --upgrade pip \
      && pip3 install --upgrade awscli \
        ansible=="${ANSIBLE_VERSION}" \
        openshift \
        setuptools \
      && pip3 --no-cache-dir install -U boto \
        boto3 \
        python-dateutil \
      && find /usr/lib/ -name '__pycache__' -print0 | xargs -0 -n1 rm -rf \
      && find /usr/lib/ -name '*.pyc' -print0 | xargs -0 -n1 rm -rf
