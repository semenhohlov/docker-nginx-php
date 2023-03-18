FROM nginx

COPY nginx.conf /etc/nginx/
COPY default.conf /etc/nginx/conf.d/

# add user and group
RUN groupadd -g 1001 develop
RUN useradd -g develop develop

RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

EXPOSE 80