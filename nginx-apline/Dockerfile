FROM alpine:3.12
RUN apk update && apk add nginx \
&& rm -rf /var/cache/apk/*
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./default.conf /etc/nginx/conf.d/default.conf

WORKDIR /usr/share/nginx/html

RUN echo "test NGINX instance inside Docker" > /usr/share/nginx/html/index.html

EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]