# Contributing

## Dev environment

Build image used as targeted nodes
```shell
cd .config/target_hosts
docker build .
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
cd /app/roles/install-pc

# Run Molecule tests
molecule test
```