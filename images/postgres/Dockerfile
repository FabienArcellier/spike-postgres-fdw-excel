FROM postgres:16

RUN apt update; apt-get install -y postgresql-server-dev-16 python3-pip
RUN apt-get install -y wget

RUN wget https://github.com/pgsql-io/multicorn2/archive/refs/tags/v2.5.tar.gz
RUN tar -xvf v2.5.tar.gz

RUN mkdir -p /fabien_fdw
COPY ./fabien_fdw /fabien_fdw

RUN cd /multicorn2-2.5; make; make install
RUN cd /fabien_fdw; pip3 install --break-system-packages -e .