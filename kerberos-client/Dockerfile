FROM debian:buster

ENV DEBIAN_FRONTEND noninteractive
# The -qq implies --yes
RUN apt-get -qq update
RUN apt-get -qq install apt-transport-https locales krb5-user curl vim
RUN apt-get -qq clean

RUN locale-gen "en_US.UTF-8"
RUN echo "LC_ALL=\"en_US.UTF-8\"" >> /etc/default/locale

ENV REALM ${REALM:-DEV.LOCAL}
ENV KADMIN_PRINCIPAL ${KADMIN_PRINCIPAL:-kadmin/admin}
ENV KADMIN_PASSWORD ${KADMIN_PASSWORD:-eskerby}

COPY init-script.sh configureKerberosClient.sh /tmp/
RUN chmod +x /tmp/configureKerberosClient.sh
RUN chmod +x /tmp/init-script.sh
CMD /tmp/init-script.sh; 'bash'
