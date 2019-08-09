FROM node:8.9

RUN npm config set registry https://registry.npm.taobao.org

RUN mkdir -p /var/www/codo-ui
WORKDIR /var/www/
RUN git clone https://github.com/xx-codo/codo
#ADD . /var/www/codo
WORKDIR /var/www/codo
RUN npm install

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "-vvv", "-g", "-w", "--"]

CMD ['/usr/local/bin/npm', 'run', 'dev']
# docker run -d -P --name=vue-admin actanble/vue-element-admin npm run dev
