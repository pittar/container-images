FROM registry.access.redhat.com/ubi8/openjdk-17:latest

USER root

RUN microdnf install -y openssh-clients git git-lfs shadow-utils
RUN groupadd -r -g 65532 nonroot && useradd --no-log-init -r -u 65532 -g nonroot -d /home/git -m nonroot

USER 65532
