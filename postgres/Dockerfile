FROM grayzone/centos

MAINTAINER Albert Wang

RUN yum -y install postgresql-server postgresql postgresql-contrib supervisor; yum clean all

#ADD ./postgresql-setup /usr/bin/postgresql-setup
#ADD ./supervisord.conf /etc/supervisord.conf
#ADD ./start_postgres.sh /start_postgres.sh

#Sudo requires a tty. fix that.
#RUN sed -i 's/.*requiretty$/#Defaults requiretty/' /etc/sudoers
#RUN chmod +x /usr/bin/postgresql-setup
#RUN chmod +x /start_postgres.sh
USER postgres

RUN /usr/bin/initdb /var/lib/pgsql/data/
#RUN postgresql-setup initdb

RUN chown -v postgres.postgres /var/lib/pgsql/data/postgresql.conf


#RUN /usr/bin/initdb /var/lib/pgsql/data/

RUN echo "host    all             all             0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf
RUN echo "listen_addresses='*'" >> /var/lib/pgsql/data/postgresql.conf

#RUN /usr/bin/pg_ctl start -D /var/lib/pgsql/data -s -o "-p 5432" -w -t 300

VOLUME ["/var/lib/pgsql/data"]

EXPOSE 5432

CMD ["/usr/bin/pg_ctl", "-D", "/var/lib/pgsql/data"]

