FROM centos:latest

RUN yum update -y && \
    yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum install -y sudo python python-pip python-virtualenv gcc make gcc-c++ && \
    useradd -u 65500 -m rally && \
    echo "rally ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/00-rally-user && \
    mkdir /rally && chown -R rally:rally /rally

RUN pip install -U setuptools pip ipaddress && \
    pip install rally-openstack && \
    mkdir -p /etc/rally && \
    echo "[database]" > /etc/rally/rally.conf && \
    echo "connection=sqlite:////home/rally/.rally/rally.db" >> /etc/rally/rally.conf
    
USER rally
ENV HOME /home/rally
RUN mkdir -p /home/rally/.rally && rally db recreate

VOLUME ["/home/rally/.rally"]
ENTRYPOINT ["rally"]
