FROM alpine:3.12

LABEL maintainer="ZhuoZhang-2021/11/02"

RUN echo "http://mirrors.ustc.edu.cn/alpine/v3.12/main/" > /etc/apk/repositories && \
      apk add --no-cache tzdata libc6-compat unzip && \
      ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
      echo "Asia/Shanghai" >> /etc/timezone && \
      echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf && \
      wget https://github.com/cookieY/Yearning/releases/download/2.3.5/Yearning-2.3.5-linux-amd64.zip && \
      unzip Yearning-2.3.5-linux-amd64.zip && \
      mv Yearning /opt/Yearning && \
      mv conf.toml /opt/conf.toml

WORKDIR /opt

CMD /opt/Yearning install && /opt/Yearning run
