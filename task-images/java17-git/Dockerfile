FROM registry.access.redhat.com/ubi8/openjdk-17:latest

USER root

RUN microdnf install -y openssh-clients git git-lfs shadow-utils

USER 65532
