from python:3.11-alpine3.18
RUN apk update && apk add --no-cache supervisor bash
RUN addgroup -S apigroup && adduser -S api -G apigroup -s /bin/bash
RUN echo "api ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN mkdir -p /home/fastapi/app/api
WORKDIR /home/fastapi/app/api
RUN mkdir project
ADD project/* ./project/
ADD requirements/* ./
ADD prod.sh ./
COPY supervisord.conf /etc/supervisord.conf
RUN pip install -r prod.txt
RUN chown -R api:apigroup /home/fastapi
RUN touch /usr/supervisord.log
RUN chown api:apigroup /usr/supervisord.log
USER api
RUN chmod -x prod.sh