FROM centos:7

MAINTAINER Shaun Hare <shaun@phpminds.org>

#
# Import the Centos-7 RPM GPG key to prevent warnings and Add EPEL Repository
#
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7 \
    && rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7 \
    && rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm

RUN yum-config-manager --enable remi-php70

RUN yum -y install \
    mysql-devel \
    mysql-libs \
    mod_ssl \
    php \
    php-fpm \
    php-curl \
    php-cli \
    php-mbstring \
    php-mcrypt \
    php-mysql \
    php-xml \
    msmtp \
    php-pecl-xdebug \
    && yum -y update bash \
    && rm -rf /var/cache/yum/* \
    && yum clean all


# UTC Timezone & Networking
#
RUN ln -sf /usr/share/zoneinfo/UTC /etc/localtime \
    && echo "NETWORKING=yes" > /etc/sysconfig/network



EXPOSE 9000
EXPOSE 9009

COPY chrome-repo /etc/yum.repos.d/google-chrome.repo

RUN yum  -y install google-chrome-stable 

#CMD ["php-fpm","-F"]

# Add chrome user
RUN groupadd -r chrome && useradd -r -g chrome -G audio,video chrome \
    && mkdir -p /home/chrome/Downloads && chown -R chrome:chrome /home/chrome


# Run Chrome as non privileged user
USER chrome

CMD ["google-chrome"]


