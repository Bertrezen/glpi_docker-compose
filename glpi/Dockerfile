FROM debian:buster
#FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive

ENTRYPOINT ["/opt/entrypoint.sh"]

RUN cd /tmp/ \
  && apt-get update -qqy \
  && apt-get upgrade -qqy \
  && apt-get install -y wget gnupg2 lsb-release \
  && wget https://packages.sury.org/php/apt.gpg && apt-key add apt.gpg \
  && echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list \
# локаль
  && apt-get install -yqq  --no-install-recommends --no-install-suggests locales apt-utils

ENV LANG='ru_RU.UTF-8' LANGUAGE='ru_RU.UTF-8' LC_ALL='ru_RU.UTF-8'
RUN echo ru_RU.UTF-8 UTF-8 >> /etc/locale.gen && locale-gen

RUN cd /tmp/ \
 # timezone
  && ln -sf /usr/share/zoneinfo/Asia/Yekaterinburg  /etc/localtime && dpkg-reconfigure -f noninteractive tzdata \
 # install
  && apt-get update -qqy \
  && apt-get -y install \
    apache2 \
    php8.2 \
    php8.2-mysql \
    php8.2-ldap \
    php8.2-xmlrpc \
    php8.2-imap \
    curl \
    php8.2-curl \
    php8.2-gd \
    php8.2-mbstring \
    php8.2-xml \
#    php8.2-apcu-bc \
#    php8.2-cas \
    php8.2-zip \
    cron \
    rsyslog \
    wget \
    graphviz \
    php8.2-snmp \
    php8.2-intl \
    php8.2-bz2
RUN cd /tmp/ \
#    miredo \
#  && echo "deb http://debian.fusioninventory.org/debian/ jessie main" >> /etc/apt/sources.list.d/fusioninventory.list \
#  && echo "deb http://debian.fusioninventory.org/debian/ buster main" >> /etc/apt/sources.list.d/fusioninventory.list \
  && apt-get update -qqy \
  && apt-get -y install gnupg2 \
#  && wget -O - http://debian.fusioninventory.org/debian/archive.key | apt-key add - \
#  && apt-key adv --keyserver keyserver.ubuntu.com --recv 049ED9B94765572E \
  && apt-get -y --allow-unauthenticated install \
    lsb-release \
    libfusioninventory-agent-task-esx-perl \
  ## clean
  && apt-get autoremove -qqy \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/*

COPY entrypoint.sh /opt/
RUN chmod +x /opt/entrypoint.sh
