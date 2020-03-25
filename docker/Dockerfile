FROM amazonlinux

RUN yum update -y
RUN yum groupinstall -y "Development Tools"
RUN yum install -y wget
RUN yum install -y openssl-libs openssl-devel openssl
RUN yum install -y zlib zlib-devel
RUN yum install -y libffi-devel

WORKDIR /build

RUN wget https://www.python.org/ftp/python/3.8.2/Python-3.8.2.tgz
RUN wget https://ftp.postgresql.org/pub/source/v9.4.3/postgresql-9.4.3.tar.gz
RUN git clone https://github.com/psycopg/psycopg2.git

RUN tar zxf Python-3.8.2.tgz
RUN tar zxf postgresql-9.4.3.tar.gz

WORKDIR /build/Python-3.8.2
RUN ./configure --enable-optimizations
RUN make altinstall
RUN python3.8 --version

WORKDIR /build/postgresql-9.4.3
RUN ./configure --without-readline --without-zlib --with-openssl
RUN make
RUN make install

WORKDIR /build/psycopg2
RUN mv setup.cfg setup.cfg.bak
COPY setup.cfg ./

RUN python3.8 setup.py build

WORKDIR /build/psycopg2/build/lib.linux-x86_64-3.8/psycopg2
RUN zip -9 /build/psycopg2.zip *

WORKDIR /build

RUN echo "Build completed. Download /build/psycopg2.zip"
