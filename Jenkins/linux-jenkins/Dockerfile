FROM jenkins/jenkins

COPY files/plugins.txt /usr/share/jenkins/ref
# COPY files/custom.groovy /usr/share/jenkins/ref/init.groovy.d/custom.groovy
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
