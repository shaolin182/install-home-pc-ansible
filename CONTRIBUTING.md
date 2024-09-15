# Contributing

## Pre requisites

On your local machine, you must install
- Docker
- VirtualBox

## Dev environment

Build image used as targeted nodes
```shell
cd .config/target_hosts
docker build -t ubuntu_python:24.04 .
```

Run dev environment
```shell
cd .config/docker
docker compose --remove-orphans up --build -d
```

## Run tests

From python-dev-container container, run those commands
```shell

# Go to role to test
cd /app/ansible_collections/jgirard/install_pc/extensions

# Run Molecule tests
molecule test
```