FROM ubuntu:trusty

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update

# Setup User
RUN useradd --home /home/worker -M worker -K UID_MIN=1000 -K GID_MIN=1000 -s /bin/bash && \
  mkdir /home/worker && \
  chown worker:worker /home/worker && \
  adduser worker sudo && \
  echo 'worker ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER worker

# Install RVM
RUN sudo apt-get install -y -q curl
RUN gpg --keyserver hkp://pgp.mit.edu --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN \curl -sSL https://get.rvm.io | bash -s stable
RUN /bin/bash -l -c 'source ~/.rvm/scripts/rvm'

# Install Ruby
RUN /bin/bash -l -c 'rvm requirements && rvm install 2.3.0 && rvm install 1.9.3 --patch railsexpress'
RUN echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"' >> /home/worker/.bashrc

# Install my deps
RUN sudo apt-get install -y -q \
    ssh \
    libxslt-dev \
    libxml2-dev \
    libcurl3-dev \
    libmagickwand-dev \
    imagemagick \
    catdoc \
    enca \
    libmysqlclient-dev \
    libpq-dev \
    time

WORKDIR /home/worker
VOLUME /home/worker
ENTRYPOINT /bin/bash
