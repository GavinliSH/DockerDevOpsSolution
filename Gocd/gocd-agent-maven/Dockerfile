FROM gocd/gocd-agent-centos-7:v18.10.0
MAINTAINER xiaoguang.li

# 变量
ENV jdk_version=jdk1.8.0_191
ENV jdk_package=jdk-8u191-linux-x64.tar.gz
ENV mvn_package=apache-maven-3.5.4-bin.tar.gz
ENV mvn_version=apache-maven-3.5.4


# 安装JDK
RUN mkdir /var/tmp/jdk
COPY "packages/${jdk_package}" /var/tmp/jdk 
# RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"  -P /var/tmp/jdk http://download.oracle.com/otn/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz
RUN tar xzf "/var/tmp/jdk/${jdk_package}" -C /var/tmp/jdk
ENV JAVA_HOME "/var/tmp/jdk/${jdk_version}"
ENV PATH $PATH:$JAVA_HOME/bin

# 安装maven
RUN mkdir /var/tmp/maven
COPY "packages/${mvn_package}" /var/tmp/maven
RUN tar xzvf "/var/tmp/maven/${mvn_package}" -C /var/tmp/maven
ENV MVN_HOME "/var/tmp/maven/${mvn_version}"
ENV PATH $PATH:$MVN_HOME/bin


# SSH keys
RUN mkdir /home/go/.ssh
COPY files/keys/* /home/go/.ssh/
# automatic add cert to known_hosts
RUN echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config
RUN chown -R go:go /home/go/.ssh
