FROM registry.centos.org/centos/centos:7

ENV OCP_VERSION=3.7

ADD bin/sign-image /usr/local/bin/

RUN rpm -ihv https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum clean all && \
    yum repolist  && \
    INSTALL_PKGS="docker atomic jq  tar" && \
    yum install -y $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all

RUN yum install -y golang openscap-scanner git bash-completion

RUN rpm -ihv http://mirror.centos.org/centos/7/paas/x86_64/openshift-origin/origin-clients-3.7.1-2.el7.x86_64.rpm
RUN mkdir -p /go/src/github.com/openshift/ && cd /go/src/github.com/openshift/ && \
    git clone https://github.com/openshift/image-inspector.git

WORKDIR /go/src/github.com/openshift/image-inspector


RUN GOBIN=/usr/bin \
    GOPATH=/go \
    CGO_ENABLED=0 \
    go install -a -installsuffix cgo /go/src/github.com/openshift/image-inspector/cmd/image-inspector.go && \
    mkdir -p /var/lib/image-inspector



# RUN yum install -y origin-clients
# RUN yum install -y  image-inspector
