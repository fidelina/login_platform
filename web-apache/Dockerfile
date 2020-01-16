# Using alpine linux as the base image
FROM alpine:3.11.2

ARG GIT_COMMIT=unknown
ENV GIT_COMMIT=${GIT_COMMIT}

# Install the required resources for the apache container to run
RUN adduser -u 1001 -g 1001 apache -D; \
        mkdir /app;  \
        chown apache.apache /app; \
        apk add --no-cache apache2 ; \
        chown -R apache.apache /etc/apache2/

COPY httpd.conf /home/apache
COPY homework.html /app

RUN chown -R apache.apache  /home/apache; \
    chown -R apache.apache /app;  \
    chown -R apache.apache /run/apache2

USER 1001

EXPOSE  8000

# To start apache in the background as a service
CMD ["/usr/sbin/httpd", "-f", "/home/apache/httpd.conf"]
ENTRYPOINT ["/usr/bin/tail", "-f", "/home/apache/error.log"]