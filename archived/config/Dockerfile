FROM centos:latest

LABEL Component="ansible,nginx,tools" \
      Name="baburajk/devops" 

ENV base /usr/share/artifacts
ENV diran ${base}/ansible
ENV dirng ${base}/nginx


RUN yum -y update && yum clean all
RUN yum -y install epel-release  \
    && yum install -y https://centos7.iuscommunity.org/ius-release.rpm \
    && yum install -y python36u python36u-libs python36u-devel python36u-pip \
    && yum -y install nginx \
    && yum -y install ansible

# pipenv installation
RUN pip3.6 install pipenv
RUN ln -s /usr/bin/pip3.6 /bin/pip
RUN rm /usr/bin/python
# python must be pointing to python3.6
RUN ln -s /usr/bin/python3.6 /usr/bin/python

RUN pip install --upgrade pip


WORKDIR  /app
COPY ./config/requirements.txt /app

#Copy ansible files 
COPY ./files/ansible/test /etc/ansible/
COPY ./files/ansible/prod /etc/ansible/


RUN pip install --trusted-host pypi.python.org -r requirements.txt

RUN mkdir -pv ${dirng}
RUN mkdir -pv ${diran} 



ADD --chown=nginx:nginx files/* /${dirng}/


#ENTRYPOINT [ "/bin/ping", "-c", "3" ]
#CMD ["localhost"]

#ENTRYPOINT [ "/bin/bash" ]
#CMD ["ls -l"]
