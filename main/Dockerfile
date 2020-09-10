FROM jenkins/jenkins:lts
LABEL maintainer="MaksSych@gmail.com"

USER root
RUN  mkdir -p /tmp/download && \ 
        curl -L https://download.docker.com/mac/static/stable/x86_64/docker-19.03.12.tgz | tar -xz -C /tmp/download && \
        rm -rf /tmp/download/docker/dockerd && \
        mv /tmp/download/docker/docker* /usr/local/bin/ && \
        rm -rf /tmp/download && \
        groupadd -g 999 docker && usermod -aG staff,docker jenkins 
USER jenkins
