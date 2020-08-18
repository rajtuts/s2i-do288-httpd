FROM registry.access.redhat.com/ubi8/ubi:8.0

LABEL Component="httpd" \
    Name="s2i-do288-httpd" \
    Version="1.0" \
    Release="1" \
    io.k8s.description="A basic Apache HTTP Server S2I builder image" \
    io.k8s.display-name="Apache HTTP Server S2I builder image for DO288" \
    io.openshift.expose-services="8080:http" \
    io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
    io.openshift.tags="builder,httpd,httpd24"

ENV DOCROOT /var/www/html
ENV APP_DIRS /var/www/ /run/httpd/ /etc/httpd/logs/ /var/log/httpd/

COPY s2i/bin /usr/libexec/s2i
RUN yum install -y --nodocs --disableplugin=subscription-manager httpd && \
    yum clean all --disableplugin=subscription-manager -y && \
    echo "This is the default index page from the s2i-do-288-httpd S2I builder image." > ${DOCROOT}/index.html && \
    sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf && \
    chown -R 1001:1001 $APP_DIRS && \
    chgrp -R 0 $APP_DIRS && \
    chmod -R g=u $APP_DIRS && \
    chmod +x /usr/libexec/s2i/assemble /usr/libexec/s2i/run /usr/libexec/s2i/usage

USER 1001
EXPOSE 8080
CMD ["usage"]
