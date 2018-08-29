FROM alpine:3.7

RUN apk --no-cache add nginx
COPY nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /run/nginx

RUN mkdir -p /var/www/site
COPY index.html /var/www/site/index.html
COPY htpasswd /var/www/site/.htpasswd

RUN mkdir -p /var/ssl
COPY ssl/cert.pem /var/ssl/cert.pem
COPY ssl/key.pem /var/ssl/key.pem

EXPOSE 443
CMD ["nginx", "-g", "daemon off;"]
