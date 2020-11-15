FROM nginx:1.17

EXPOSE 8000
RUN apt-get update && apt-get install -y wget

COPY nginx.conf /etc/nginx/nginx.conf

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && wget https://github.com/tkuchiki/alp/releases/download/v0.3.1/alp_linux_amd64.zip \
    && apt install unzip \
    && unzip alp_linux_amd64.zip \
    && install ./alp /usr/local/bin