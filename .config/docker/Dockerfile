FROM docker.io/python:3.12.5

# Docker cli is mandatory for running command 'molecule converge'
# Without Docker cli, create of hosts from file 'molecule/default/create.yml' fails on step 'Validate that inventory was refreshed'
# Error met is 'docker not command not found in PATH'
COPY --from=docker:cli /usr/local/bin/docker /usr/local/bin/

RUN python3 -m pip install --user ansible

# For dev purpose only
RUN python3 -m pip install --user molecule ansible-dev-tools
RUN python3 -m pip install --trusted-host pypi.org --user "molecule-plugins[docker]"

ENV PATH=$PATH:/root/.local/bin

RUN mkdir -p /app