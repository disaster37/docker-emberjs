FROM ubuntu:15.04
MAINTAINER Sebastien Langoureaux <linuxworkgroup@hotmail.com>

ENV NODEJS_VERSION 0.12
ENV WEBSTORM_VERSION 10.0.4



RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install software-properties-common -y && \
    update-locale LANG=C.UTF-8 LC_MESSAGES=POSIX && \
    locale-gen en_US.UTF-8 && \
    dpkg-reconfigure locales

# Install Nodejs, Java, Maven, Git, terminal, etc.
RUN apt-get install curl openjdk-7-jre xfce4-terminal git unzip make libkrb5-dev -y
RUN apt-get install build-essential -y

RUN curl -sL https://deb.nodesource.com/setup_${NODEJS_VERSION} | bash -
RUN apt-get install -y nodejs


# Upgrade nodejs lib
RUN npm install -g async

# Install npm module
RUN npm install -g yo bower grunt-cli gulp ember-cli watchman express-generator nodemon node-gyp generator-angular-fullstack

# Install Webstorm IDEA

RUN curl http://download.jetbrains.com/webstorm/WebStorm-${WEBSTORM_VERSION}.tar.gz -Lo "/tmp/webstorm.tar.gz"

RUN mkdir -p /opt/webstorm
RUN tar -xf /tmp/webstorm.tar.gz --strip-components=1 -C /opt/webstorm
RUN rm /tmp/webstorm.tar.gz
RUN ln -s /opt/webstorm/bin/webstorm.sh /usr/bin/webstorm




# CLEAN APT
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Create user and folder to work
RUN useradd -m dev
USER dev


WORKDIR /home/dev
EXPOSE 4200
VOLUME ["/home/dev/"]
CMD ["webstorm"]
