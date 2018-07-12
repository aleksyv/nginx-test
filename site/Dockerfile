FROM alpine:3.7

RUN apk --no-cache add nginx
COPY nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /run/nginx

RUN mkdir -p /var/www/site
COPY index.html /var/www/site/index.html
COPY htpasswd /var/www/site/.htpasswd

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
