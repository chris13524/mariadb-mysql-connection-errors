FROM mariadb:10.2.18

ARG DATABASE_ROOT_PASS=password
ARG KILLBILL_DATABASE_NAME=killbill
ARG KILLBILL_DATABASE_USER=killbill
ARG KILLBILL_DATABASE_PASS=password

ENV MYSQL_ROOT_PASSWORD=$DATABASE_ROOT_PASS

COPY mysql.cnf /etc/mysql/conf.d/mysql.cnf
 # starts with aa so `for` will list it first
COPY install.sql   /docker-entrypoint-initdb.d/aa_install.sql
COPY killbill.sql  /docker-entrypoint-initdb.d/killbill.sql

RUN sed -i -e "s|\$KILLBILL_DATABASE_NAME|$KILLBILL_DATABASE_NAME|g" /docker-entrypoint-initdb.d/aa_install.sql && \
    sed -i -e "s|\$KILLBILL_DATABASE_USER|$KILLBILL_DATABASE_USER|g" /docker-entrypoint-initdb.d/aa_install.sql && \
    sed -i -e "s|\$KILLBILL_DATABASE_PASS|$KILLBILL_DATABASE_PASS|g" /docker-entrypoint-initdb.d/aa_install.sql && \
    sed -i "1i USE $KILLBILL_DATABASE_NAME;" /docker-entrypoint-initdb.d/killbill.sql
