FROM registry.access.redhat.com/ubi9/python-311:latest

ENV OC_VERSION=stable-4.13 \
    YQ_VERSION=v4.35.1 \
    YQ_BINARY=yq_linux_amd64

USER root

# Curl already exists, but add:
#    * JQ, wget, openssl and skopeo
#    * More to come...
RUN dnf makecache && \
    dnf install -y \
    openssl wget jq skopeo \
    && dnf clean all && rm -rf /var/cache/dnf/*

# Kube dir.
RUN mkdir -p ~/.kube && \
    chgrp -R 0 ~/.kube && \
    chmod -R g+rwX ~/.kube

# oc and kubectl
RUN curl -s https://mirror.openshift.com/pub/openshift-v4/clients/ocp/$OC_VERSION/openshift-client-linux.tar.gz | tar -xz && \
    mv oc /usr/bin/oc && \
    mv kubectl /usr/bin/kubectl

# Install the latest AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm awscliv2.zip

# yq
RUN wget https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/${YQ_BINARY}.tar.gz -O - | \
    tar xz && \
    mv ${YQ_BINARY} \
    /usr/bin/yq

USER 1001
