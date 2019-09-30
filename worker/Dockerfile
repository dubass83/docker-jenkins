FROM ubuntu:18.04
LABEL maintainer="MaksSych@gmail.com"

RUN apt-get update && \
    apt-get install -y openssh-server locales openjdk-8-jdk openjdk-8-jre-headless git make curl && \
    mkdir /var/run/sshd && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /etc/ssh/ssh_host_*
ENV LANG=en_US.utf8
RUN echo "$LANG UTF-8" >> /etc/locale.gen && \
    locale-gen && \
    update-locale --reset LANG=$LANG
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates software-properties-common && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce
ENV JENKINS_HOME=/var/jenkins_home
ENV JAVA_TOOL_OPTIONS=-Dfile.encoding=UTF8
ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000
#|4 gid=1000 group=jenkins uid=1000 user=jenkins 
RUN groupadd -g ${gid} ${group} && \
    useradd -d "$JENKINS_HOME" -u ${uid} -g ${gid} -m -s /bin/bash ${user}
VOLUME [/var/jenkins_home]
#|4 gid=1000 group=jenkins uid=1000 user=jenkins 
RUN usermod -aG docker jenkins
EXPOSE 22
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]