FROM montge/centos-java8

# COPY Logstash yum repo
COPY logstash.repo /etc/yum.repos.d/

# install plugin dependencies
RUN yum update && yum install -y logstash && yum clean all

ENV PATH /opt/logstash/bin:$PATH

# Install gosu - https://github.com/tianon/gosu
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN set -x
RUN curl -L https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64 -o /usr/local/sbin/gosu;
RUN curl -L https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64.asc -o /usr/local/sbin/gosu.asc;
RUN gpg --verify /usr/local/sbin/gosu.asc
RUN rm /usr/local/sbin/gosu.asc
RUN chmod 0755 /usr/local/sbin/gosu

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["logstash", "agent"]
