############################################################
# Dockerfile for basic rpmbuild set-up
# Based on CentOS 7
############################################################


# Set the base image to centos
FROM centos:7

# File Author / Maintainer
MAINTAINER Lars Kiesow <lkiesow@uos.de>


# Update the repository sources list
RUN yum -y update
RUN yum -y install git tmux ctags vim-enhanced wget curl zsh
RUN yum -y install createrepo rpmdevtools rpmlint yum-utils rpm-sign epel-release
RUN yum -y groupinstall 'Development Tools'

# User set-up
RUN useradd -s /bin/zsh makerpm
RUN rm -rf /home/makerpm/.zshrc
RUN usermod -s /bin/zsh root

# Clone system configuration
RUN git clone https://github.com/lkiesow/system-configuration.git /etc/system-configuration
RUN ln -s /etc/system-configuration /root/system-configuration
RUN ln -s /etc/system-configuration /home/makerpm/system-configuration

# Activate configuration
RUN /root/system-configuration/install.sh
RUN su -c '/home/makerpm/system-configuration/install.sh' makerpm

# Prepare rpmbuild
RUN su -c 'rpmdev-setuptree' makerpm


##################### INSTALLATION END #####################

# Expose the default port
CMD ["/bin/zsh"]
