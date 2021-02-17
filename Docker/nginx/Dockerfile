FROM nginx
RUN apt-get update && apt-get install -y vim
COPY nginx.conf /etc/nginx/nginx.conf
COPY redirect.map /etc/nginx/redirect.map