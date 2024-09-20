FROM docker.io/ubuntu:24.04

# Docker cli is mandatory for running command 'molecule converge'
# Without Docker cli, create of hosts from file 'molecule/default/create.yml' fails on step 'Validate that inventory was refreshed'
# Error met is 'docker not command not found in PATH'
COPY --from=docker:cli /usr/local/bin/docker /usr/local/bin/

# Install Python
RUN apt-get update
RUN apt-get -y install wget python3 python3-pip

# Install ansible and its dependencies
RUN python3 -m pip install --break-system-packages --user ansible

# Install ansible dev plugins
RUN python3 -m pip install --break-system-packages --user molecule ansible-dev-tools
RUN python3 -m pip install --break-system-packages --trusted-host pypi.org --user "molecule-plugins[docker]"
RUN python3 -m pip install --break-system-packages --trusted-host pypi.org --user "molecule-plugins[vagrant]"

# Install Vagrant
RUN wget -O- https://apt.releases.hashicorp.com/gpg -O- | apt-key add
RUN sh -c 'echo "deb https://apt.releases.hashicorp.com noble main" >> /etc/apt/sources.list.d/hashicorp.list'
RUN apt-get update
RUN apt-get install -yy vagrant

## Install VirtualBox
RUN sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian noble contrib" >> /etc/apt/sources.list.d/virtualbox.list'
RUN wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox_2016.asc -O- | apt-key add -
RUN apt-get update
RUN apt-get install -y virtualbox
RUN apt-get install -y -f

# Install Virtualbox Extension Pack
RUN VBOX_VERSION=`dpkg -s virtualbox | grep '^Version: ' | sed -e 's/Version: \([0-9\.]*\)\-.*/\1/'` ; \
    wget http://download.virtualbox.org/virtualbox/${VBOX_VERSION}/Oracle_VM_VirtualBox_Extension_Pack-${VBOX_VERSION}.vbox-extpack ; \
    VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-${VBOX_VERSION}.vbox-extpack ; \
    rm Oracle_VM_VirtualBox_Extension_Pack-${VBOX_VERSION}.vbox-extpack

RUN apt-get install -y openssh-client

# The virtualbox driver device must be mounted from host
VOLUME /dev/vboxdrv

ENV PATH=$PATH:/root/.local/bin

RUN mkdir -p /app