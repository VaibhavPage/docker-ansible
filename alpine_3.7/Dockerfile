FROM alpine:3.7
MAINTAINER "Andrew Rothstein" andrew.rothstein@gmail.com

# install ansible
RUN apk update \
 && apk upgrade \
 && apk add \
   shadow \
   python3 \
   python3-dev \
   build-base \
   libffi-dev \
   openssl-dev \
   wget \
   ca-certificates \
 && wget https://bootstrap.pypa.io/get-pip.py -O /usr/local/bin/get-pip.py \
 && python3 /usr/local/bin/get-pip.py \
 && pip install urllib3 ansible==2.8.0 \
 && apk del \
   build-base \
   libffi-dev \
   openssl-dev \
 && rm -rf /var/cache/apk/*

WORKDIR /etc/ansible
# configure ansible to target the localhost -- inside the container
ADD ansible.cfg ansible.cfg

RUN mkdir -p /etc/ansible/inventories
WORKDIR /etc/ansible/inventories
ADD localhost hosts

RUN ansible --version \
 && ansible all --list-hosts \
 && ansible all -m ping
