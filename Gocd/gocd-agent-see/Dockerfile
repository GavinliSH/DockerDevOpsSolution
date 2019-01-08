FROM gocd/gocd-agent-centos-7:v18.10.0
MAINTAINER xiaoguang.li

# 变量
ARG jdk_version=jdk1.8.0_191
ARG jdk_package=jdk-8u191-linux-x64.tar.gz
ARG pmd_package=pmd-bin-6.4.0.zip
ARG python_package=Python-3.7.1.tgz
ARG python_version=Python-3.7.1

# 安装JDK
RUN mkdir /var/tmp/jdk
COPY "packages/${jdk_package}" /var/tmp/jdk 
# RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"  -P /var/tmp/jdk http://download.oracle.com/otn/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz
RUN tar xzf "/var/tmp/jdk/${jdk_package}" -C /var/tmp/jdk
ENV JAVA_HOME "/var/tmp/jdk/${jdk_version}"
ENV PATH $PATH:$JAVA_HOME/bin

# SSH keys
RUN mkdir /home/go/.ssh
COPY files/keys/* /home/go/.ssh/
# automatic add cert to known_hosts
RUN echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config
RUN chown -R go:go /home/go/.ssh

# Python3
COPY "packages/${python_package}" /usr/src
RUN yum install -y deltarpm \
    && yum install -y gcc openssl-devel bzip2-devel zlib make python-setuptools openssl libffi-devel
RUN tar xzf "/usr/src/${python_package}" -C /usr/src \ 
    && cd "/usr/src/${python_version}" \
    && ./configure --enable-optimizations
RUN cd "/usr/src/${python_version}" \
    && make altinstall
RUN python3.7 -V

# Install pip plugins
COPY files/requirements.txt /tmp
RUN pip3.7 install -r /tmp/requirements.txt


# pmd
COPY "packages/${pmd_package}" /var/tmp/pmd/ 
RUN unzip -d /opt/pmd "/var/tmp/pmd/${pmd_package}"
RUN echo "alias pmd="/opt/pmd/pmd-bin-6.4.0/bin/run.sh pmd"" >>/root/.bashrc
RUN ["/bin/bash", "-c", "source /root/.bashrc"]

ARG node_package=node-v8.9.4-linux-x64.tar.xz
ARG node_file=node-v8.9.4-linux-x64

# 安装node
RUN mkdir /var/tmp/node
COPY "packages/${node_package}" /var/tmp/node
RUN tar xf "/var/tmp/node/${node_package}" -C /var/tmp/node
ENV NODE_HOME "/var/tmp/node/${node_file}"
ENV PATH $PATH:$NODE_HOME/bin 
ENV NODE_PATH $NODE_HOME/lib/node_modules

RUN node -v
RUN npm -v

RUN npm install babel-eslint eslint -g \
    # Installing tslint ...
    npm install tslint@4.5.1 typescript@2.1.5 -g \
    npm install tslint-clean-code@0.2.7 -g \
    npm install eslint-plugin-import@latest -g