FROM ubuntu:16.04

ENV ANSIBLE_VERSION="2.9.12-1ppa~xenial"

# Install ansible and clean up apt when done.
RUN apt-get update -y \
      && apt-get install -y software-properties-common \
      && add-apt-repository ppa:ansible/ansible-2.9 -y \
      && apt-get update -y \
      && apt-get install -y ansible="${ANSIBLE_VERSION}" \
        python-pip \
        python-dev \
        build-essential \
        git \
        jq \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
   
# Install boto
RUN pip install --upgrade pip \
      && pip install --upgrade awscli \
        openshift \
      && pip --no-cache-dir install -U boto \
        boto3 \
        python-dateutil \
      && find /usr/lib/ -name '__pycache__' -print0 | xargs -0 -n1 rm -rf \
      && find /usr/lib/ -name '*.pyc' -print0 | xargs -0 -n1 rm -rf
