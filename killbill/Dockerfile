FROM killbill/killbill:0.18.21

ARG KILLBILL_DATABASE_NAME=killbill
ARG KILLBILL_DATABASE_USER=killbill
ARG KILLBILL_DATABASE_PASS=password
ARG KILLBILL_USER=admin
ARG KILLBILL_PASS=password

COPY killbill.properties /etc/killbill/killbill.properties
COPY shiro.ini /var/tmp/shiro.ini

# fix permissions of copied files
USER root
RUN chown tomcat7:tomcat7 /etc/killbill/killbill.properties && \
    chown tomcat7:tomcat7 /var/tmp/shiro.ini
USER tomcat7

# set configuration
RUN sed -i -e "s|\$KILLBILL_DATABASE_NAME|$KILLBILL_DATABASE_NAME|g" /etc/killbill/killbill.properties && \
    sed -i -e "s|\$KILLBILL_DATABASE_USER|$KILLBILL_DATABASE_USER|g" /etc/killbill/killbill.properties && \
    sed -i -e "s|\$KILLBILL_DATABASE_PASS|$KILLBILL_DATABASE_PASS|g" /etc/killbill/killbill.properties && \
    sed -i -e "s|\$KILLBILL_USER|$KILLBILL_USER|g" /var/tmp/shiro.ini && \
    sed -i -e "s|\$KILLBILL_PASS|$KILLBILL_PASS|g" /var/tmp/shiro.ini

# pre-install the plugins
RUN bash -c '(cat /etc/init.d/killbill.sh | sed "s|exit 1|echo not exiting|g" && echo "install") | . /dev/stdin'
