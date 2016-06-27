FROM centos:5

MAINTAINER nimmis <kjell.havneskold@gmail.com>

# disable interactive functions
ENV DEBIAN_FRONTEND noninteractive

RUN yum update -y && \
    rpm -Uhv http://dl.fedoraproject.org/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm && \
    yum install -y git && \
    # Create autorun directories
    mkdir /etc/my_runonce && mkdir /etc/my_runalways && \

    # moved all configuration to separate git repository
    git clone https://github.com/nimmis/docker-utils.git && \
    # run os fixes for Ubuntu
    docker-utils/centos/root/fix.sh && \
    # copy configuration files and commands to disk
    cp -p docker-utils/centos/bin/* /usr/local/bin/ && \
    cp -p docker-utils/centos/my_runonce/* /etc/my_runonce/ && \
    cp -p docker-utils/centos/root/my* / && \
    cp -pR docker-utils/centos/supervisor/* /etc/ && \
    # remove repository from image
    rm -Rf docker-utils && \
    # remove extra space from git command
#    apt-get remove -y git && \
#    apt-get autoremove -y && \
    # remove apt cache from image
#    apt-get clean all
    yum clean all

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["/my_init"]
