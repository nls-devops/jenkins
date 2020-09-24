FROM jenkins/jenkins:lts-alpine
USER root

#install docker
RUN apk add --update docker openrc && \
    rc-update add docker boot

#install python3
RUN apk add --no-cache python3 python3-dev curl gcc g++ libxml2-dev libxslt-dev libffi-dev && \
    ln -s /usr/include/locale.h /usr/include/xlocale.h && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools bs4 wget lxml && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

#Install ansible,  ansible-galaxy needs ansible version 2.9 
RUN apk add py3-cryptography && \
  pip3 install ansible==2.9.10 netapp-lib requests && \
  ansible-galaxy collection install netapp.ontap

USER jenkins