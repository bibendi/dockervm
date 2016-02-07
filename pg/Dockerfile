FROM postgres:9.4

RUN apt-get update

RUN apt-get -y install \
  postgresql-plperl-$PG_MAJOR=$PG_VERSION \
  postgresql-$PG_MAJOR-pgq3
