FROM docker.io/python:3.12.5

RUN python3 -m pip install --user ansible
RUN python3 -m pip install --user ansible-dev-tools

ENV PATH=$PATH:/root/.local/bin

RUN mkdir -p /app