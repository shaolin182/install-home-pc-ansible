FROM docker.io/python:3.12.5

RUN python3 -m pip install --user ansible

# For dev purpose only
RUN python3 -m pip install --user molecule ansible-dev-tools

ENV PATH=$PATH:/root/.local/bin

RUN mkdir -p /app