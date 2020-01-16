
COPY default.conf /etc/nginx/conf.d/
COPY nginx.conf /etc/nginx/

RUN mkdir /app;

COPY test.html /app/

RUN  adduser www --uid 1001 --disabled-login --disabled-password --system --no-create-home; \
     chown -R www /app; \
     chown -R www /etc/nginx; \
     chown -R www /usr/share/nginx; \
     chown -R www /var/run/*; \
     chown -R www /var/cache/nginx/;

EXPOSE 8000

USER 1001
