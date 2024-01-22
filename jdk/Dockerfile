FROM archlinux:latest

LABEL maintainer="delverjw@gmail.com"

COPY mirrorlist /etc/pacman.d/

##安装 locale 文件
RUN pacman -Syu --noconfirm

##设置 locale
#ENV LANG en_US.utf8
#ENV LANGUAGE en_US:en
#ENV LC_ALL en_US.utf8

##时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

##安装 JDK
RUN pacman -S --noconfirm wget net-tools jdk-openjdk

##清理缓存
RUN pacman -Scc --noconfirm && rm -rf /var/cache/pacman/pkg/*

##安装 Arthas
RUN wget -O /opt/arthas-boot.jar https://arthas.aliyun.com/arthas-boot.jar

##添加 SkyWalking-Agent
ARG SKYWALKING_VERSION="9.0.0"

RUN wget https://mirrors.aliyun.com/apache/skywalking/java-agent/${SKYWALKING_VERSION}/apache-skywalking-java-agent-${SKYWALKING_VERSION}.tgz \
&& tar -zxf apache-skywalking-java-agent-${SKYWALKING_VERSION}.tgz \
&& mv skywalking-agent /opt/skywalking-agent \
&& rm -rf apache-skywalking-java-agent-${SKYWALKING_VERSION}.tgz

COPY skywalking/agent.config /opt/skywalking-agent/config/

WORKDIR /
