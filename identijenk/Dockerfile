from jenkins/jenkins
 
USER root
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common 
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update  -qq \
    && apt-get install docker-ce=17.12.1~ce-0~debian -y
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

RUN usermod -aG docker jenkins

RUN curl -L https://github.com/docker/compose/releases/download/1.29.2/\
docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose; \
chmod +x /usr/local/bin/docker-compose

USER jenkins

COPY plugins.sh /usr/local/bin/plugins.sh
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/ref/plugins.txt
