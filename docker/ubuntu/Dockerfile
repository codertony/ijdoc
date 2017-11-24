FROM ubuntu:16.04
MAINTAINER tony 932010806@qq.com

# only for Chinese Developers
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak

COPY ./sources.list /etc/apt/

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C0B21F32 \
  && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 437D05B5

RUN apt-get update \
  && apt-get install -y git \
  && apt-get install -y supervisor  \
  && apt-get install -y curl sudo 

RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -

RUN apt-get install -y nodejs \
     && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
     && apt-get autoremove -y \
    && ln -s /usr/bin/nodejs /usr/local/bin/node

RUN mkdir -p /var/log/supervisor

# only for local test, copy source code of DOClever to this file, create a fold named "source", and paste codes into it.
#COPY /source /root/DOClever
RUN git clone -b 5i5j https://github.com/codertony/DOClever.git /root/DOClever

RUN alias cnpm="npm --registry=https://registry.npm.taobao.org \
    --cache=$HOME/.npm/.cache/cnpm \
    --disturl=https://npm.taobao.org/dist \
    --userconfig=$HOME/.cnpmrc"
    
RUN cd /root/DOClever && npm run cnpmInit

EXPOSE 10000

COPY ./entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
