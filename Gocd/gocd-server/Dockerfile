FROM gocd/gocd-server:v18.10.0

# Install plugins
COPY packages/plugins/*.jar /godata/plugins/external/

# SSH keys for git
RUN mkdir /home/go/.ssh
COPY files/keys/* /home/go/.ssh/
# automatic add cert to known_hosts
RUN echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config
RUN chown -R go:go /home/go/.ssh

# # Git proxy
# USER go
# ENV http_proxy=value
# ENV https_proxy=value
# RUN git config --global http.proxy ${http_proxy} \
#     && git config --global https.proxy ${https_proxy}
# USER root