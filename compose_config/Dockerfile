FROM ubuntu:20.04

RUN apt-get update
RUN apt-get install -y --no-install-recommends git 
RUN apt-get install -y --no-install-recommends python3
RUN apt-get install -y --no-install-recommends python3-pip
RUN apt-get install -y --no-install-recommends build-essential
RUN apt-get install -y --no-install-recommends wget
RUN apt-get install -y --no-install-recommends python3-dev
RUN apt-get install -y --no-install-recommends python3-venv
RUN apt-get install -y --no-install-recommends python3-wheel
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y --no-install-recommends libxslt-dev
RUN apt-get install -y --no-install-recommends libzip-dev
RUN apt-get install -y --no-install-recommends libldap2-dev
RUN apt-get install -y --no-install-recommends libsasl2-dev
RUN apt-get install -y --no-install-recommends python3-setuptools
RUN apt-get install -y --no-install-recommends libjpeg-dev
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y --no-install-recommends gdebi
RUN apt-get install -y --no-install-recommends libpq-dev
RUN apt-get install -y --no-install-recommends python-dev
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y --no-install-recommends libxml2-dev
RUN apt-get install -y --no-install-recommends libxslt1-dev
RUN apt-get install -y --no-install-recommends libldap2-dev
RUN apt-get install -y --no-install-recommends libsasl2-dev
RUN apt-get install -y --no-install-recommends libffi-dev
RUN apt-get install -y --no-install-recommends postgresql
RUN apt-get install -y --no-install-recommends postgresql-contrib
RUN apt-get install -y --no-install-recommends xfonts-75dpi
RUN apt-get install -y --no-install-recommends nodejs
RUN apt-get install -y --no-install-recommends npm
RUN apt-get install -y --no-install-recommends dpkg 
RUN apt-get install -y --no-install-recommends wkhtmltopdf 

RUN  adduser --system --home=/opt/odoo --group odoo
RUN  mkdir /var/log/odoo
RUN  chown -R odoo:root /var/log/odoo
RUN  mkdir /etc/odoo

RUN git clone --depth 1 --branch master https://www.github.com/odoo/odoo /opt/odoo 
RUN chown -R odoo:odoo /opt/odoo/*

RUN  pip3 install -r /opt/odoo/requirements.txt 
RUN  npm install -g rtlcss
RUN  apt update -y

RUN  mkdir /opt/odoo/external_addons

COPY ./compose_config/odoo-server.conf /etc/odoo/
COPY ./compose_config/odoo-server.service /lib/systemd/system/
COPY ./external_addons/. /opt/odoo/external_addons/


RUN chmod 755 /lib/systemd/system/odoo-server.service \
    	&& chown root: /lib/systemd/system/odoo-server.service \
    	&& chown -R odoo: /opt/odoo/ \
    	&& chown odoo:root /var/log/odoo \
    	&& chown odoo: /etc/odoo/odoo-server.conf \
    	&& chmod 640 /etc/odoo/odoo-server.conf

USER odoo

CMD ["python3 /opt/odoo/odoo-10.0/odoo-bin -c /etc/odoo/odoo-server.conf"]

WORKDIR /opt/odoo
