FROM fedora:25
MAINTAINER "Andrew Rothstein" andrew.rothstein@gmail.com

# install ansible
RUN dnf update -y \
 && dnf install -y python wget \
 && wget https://bootstrap.pypa.io/get-pip.py -O /usr/local/bin/get-pip.py \
 && python /usr/local/bin/get-pip.py \
 && pip install urllib3 ansible==2.8.0 \
 && dnf clean all

WORKDIR /etc/ansible
# configure ansible to target the localhost -- inside the container
ADD ansible.cfg ansible.cfg

RUN mkdir -p /etc/ansible/inventories
WORKDIR /etc/ansible/inventories
ADD localhost hosts

RUN ansible --version \
 && ansible all --list-hosts \
 && ansible all -m ping
