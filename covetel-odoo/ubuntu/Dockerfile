FROM ubuntu:trusty

MANTAINER Walter Vargas "walter@covetel.com.ve"

ENV APPLICATION_NAME odoo8
ENV ENVIRONMENT test
ENV ODOO_USER odoo
ENV ODOO_HOME /home/$ODOO_USER
ENV ODOO_ADDONS_DIR $ODOO_HOME/addons

ADD odoo.list /etc/apt/sources.list.d/odoo.list
ADD sources.list /etc/apt/sources.list

RUN locale-gen en_US.UTF-8 && update-locale
RUN echo 'LANG="en_US.UTF-8"' > /etc/default/locale
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN useradd -d $ODOO_HOME -u 1000 -m -s /bin/bash $ODOO_USER

RUN apt-get update
RUN apt-get -y upgrade

RUN apt-get install -y postgresql
RUN apt-get install --allow-unauthenticated -y odoo supervisor

RUN adduser odoo postgres

USER postgres
RUN /etc/init.d/postgresql start &&\
    psql -e --command "CREATE USER $ODOO_USER WITH SUPERUSER" &&\
    /etc/init.d/postgresql stop

USER root

EXPOSE 8069