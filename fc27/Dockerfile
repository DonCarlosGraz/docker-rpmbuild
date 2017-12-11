############################################################
# Dockerfile for basic rpmbuild set-up
# Based on Fedora 26
############################################################


# Set the base image to centos
FROM fedora:27

# File Author / Maintainer
MAINTAINER Lars Kiesow <lkiesow@uos.de>


# Update the repository sources list
RUN dnf -y update
RUN dnf -y install git tmux ctags vim-enhanced wget curl zsh
RUN dnf -y install createrepo rpmdevtools rpmlint dnf-plugins-core rpm-sign
RUN dnf -y groupinstall 'Development Tools'

# Add RPMFusion
RUN dnf -y install --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-23.noarch.rpm
RUN dnf -y install --nogpgcheck http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-23.noarch.rpm

RUN useradd -s /bin/zsh makerpm
RUN git clone https://github.com/lkiesow/system-configuration.git /etc/system-configuration
RUN ln -s /etc/system-configuration /root/system-configuration
RUN /root/system-configuration/install.sh
RUN usermod -s /bin/zsh root
RUN ln -s /etc/system-configuration /home/makerpm/system-configuration
RUN su -c '/home/makerpm/system-configuration/install.sh' makerpm
RUN su -c 'rpmdev-setuptree' makerpm


##################### INSTALLATION END #####################

# Expose the default port
CMD ["/bin/zsh"]
