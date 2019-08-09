FROM python:3.6

MAINTAINER actanble <actanble@gmail.com>

# 设置编码
ENV LANG en_US.UTF-8
# 同步时间
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN mkdir -p /usr/local/src/codo

RUN git clone https://github.com/xx-codo/codo-admin && \
    git clone https://github.com/xx-codo/codo-cmdb  && \
    git clone https://github.com/xx-codo/codo-tools && \
    git clone https://github.com/xx-codo/codo-task  && \
    git clone https://github.com/xx-codo/kerrigan   && \
    git clone https://github.com/xx-codo/codo-cron  && \
    git clone https://github.com/xx-codo/codo-dns

WORKDIR /usr/local/src/codo

RUN pip3 install --upgrade pip
RUN pip3 install -U git+https://gitee.com/actanble/ops-sdk.git
RUN for x in $(find . -name 'requirements.txt' | awk '{print $1}'); do pip3 install -r $x; done

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "-vvv", "-g", "-w", "--"]
