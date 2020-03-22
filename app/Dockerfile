#FROM centos
#RUN yum install epel-release yum-utils -y
#RUN yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y
#RUN yum-config-manager --enable remi-php73 -y
#RUN yum install php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysqlnd -y
#COPY ./index.php /var/www/html
#COPY ./httpd.conf /etc/httpd/
#CMD ["/usr/sbin/httpd", "-D", "foreground"]
#EXPOSE 8000
###############
FROM centos:7
MAINTAINER The CentOS Project <cloud-ops@centos.org>
LABEL Vendor="CentOS" \
      License=GPLv2 \
      Version=2.4.6-40


RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install httpd && \
    yum clean all
RUN yum install epel-release yum-utils -y
RUN yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y
RUN yum-config-manager --enable remi-php73 -y
RUN yum install php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysqlnd -y

EXPOSE 80

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh
ADD index.php /var/www/html/index.php
ADD httpd.conf /etc/httpd/httpd.conf

CMD ["/run-httpd.sh"]
