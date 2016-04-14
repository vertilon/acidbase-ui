FROM ubuntu:14.04
MAINTAINER Mykyta Drapatyi <vertilon@gmail.com>
RUN apt-get update && apt-get -y install wget
RUN echo deb http://ppa.launchpad.net/saltstack/salt/ubuntu `lsb_release -sc` main | sudo tee /etc/apt/sources.list.d/saltstack.list
RUN wget -q -O- "http://keyserver.ubuntu.com:11371/pks/lookup?op=get&search=0x4759FA960E27C0A6" | sudo apt-key add -
RUN apt-get update
RUN apt-get -y install salt-master salt-api salt-cloud salt-minion salt-ssh
RUN apt-get -y install supervisor
RUN apt-get install -y python-pip && pip install supervisor-stdout
RUN pip install CherryPy
RUN useradd saltdev -p saltdev
RUN mkdir -p /var/log/supervisor
ADD salt-server/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

ADD salt-server/master.conf /etc/salt/master
EXPOSE 4505 4506 8080

ENTRYPOINT ["/usr/bin/supervisord"]
