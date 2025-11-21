FROM registry.access.redhat.com/ubi10/nginx-126:10.0

USER root


RUN rm -f /etc/nginx/conf.d/default.conf


RUN mkdir -p /opt/app-root/src /opt/app-root/etc


COPY index.html /opt/app-root/src/index.html
COPY nginx.conf /opt/app-root/etc/nginx.conf


RUN chmod -R 755 /opt/app-root/src /opt/app-root/etc/nginx.conf
RUN mkdir -p /var/log/nginx /var/run && chmod -R 777 /var/log/nginx /var/run

EXPOSE 8080

USER 1001

CMD ["nginx", "-c", "/opt/app-root/etc/nginx.conf", "-g", "daemon off;"]
