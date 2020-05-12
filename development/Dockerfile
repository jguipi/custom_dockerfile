FROM alpine:latest

RUN apk --no-cache add curl
RUN apk add --update bash

RUN curl -LO https://storage.googleapis.com/spinnaker-artifacts/spin/$(curl -s https://storage.googleapis.com/spinnaker-artifacts/spin/latest)/linux/amd64/spin \
    -o /usr/local/bin/spin \
    && chmod +x /usr/local/bin/spin \
    && spin /usr/local/bin/spin

ENV JQ_VERSION="jq-1.6"
RUN curl -L https://github.com/stedolan/jq/releases/download/${JQ_VERSION}/jq-linux64 \
    -o /usr/local/bin/jq \
    && chmod +x /usr/local/bin/jq \
    && jq --help

ENV YQ_VERSION="3.2.1"
RUN curl -L https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64 \
    -o /usr/local/bin/yq \
    && chmod +x /usr/local/bin/yq \
    && yq --help

# Note: Latest version of kubectl may be found at:
# https://aur.archlinux.org/packages/kubectl-bin/
ENV KUBE_LATEST_VERSION="v1.17.0"
RUN curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBE_LATEST_VERSION}/bin/linux/amd64/kubectl \
    -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl \
    && kubectl help

ENV VAULT_VERSION="1.3.2"
RUN wget https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip \
    && unzip vault_${VAULT_VERSION}_linux_amd64.zip \
    && rm vault_${VAULT_VERSION}_linux_amd64.zip \
    && mv vault /usr/local/bin \
    && vault --help

WORKDIR /config

CMD bash