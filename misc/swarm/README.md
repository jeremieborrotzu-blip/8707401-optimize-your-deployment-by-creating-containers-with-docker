# Docker Swarm in Docker

The `docker-compose.yml` file in this directory allows you to start a [Docker Swarm](https://docs.docker.com/engine/swarm/) cluster in a [Docker Compose](https://docs.docker.com/compose/) environment, meaning without having to start multiple machines with Docker.

## Start the Swarm Cluster

1. Navigate to the directory:

   ```bash
   cd misc/swarm
   ```

2. Run the command `docker compose up`

After a few seconds, the Swarm cluster should be initialized and ready to use.

## Manage the Cluster

To manage the cluster and execute Docker commands on it, two options are available.

### Enter the Container

You can enter Docker commands directly by entering the `manager` container. To do so, run:

```bash
docker compose exec manager /bin/sh
```

Then type the desired Docker commands, for example:

```bash
docker node ls
```

### Using the Host Machine's Docker Client

You can also query your Swarm cluster using the Docker client on your host machine. To do so:

```bash
# Recover permissions on the `certs/client` directory
sudo chown -R $(whoami): certs/client

# Retrieve the list of nodes in your Swarm cluster
docker --tlscacert ./certs/client/ca.pem --tlscert ./certs/client/cert.pem  --tlskey ./certs/client/key.pem --tls -H localhost:22376 node ls
```

You will need to specify the `--tlscacert`, `--tlscert`, `--tlskey`, `--tls`, and `-H` flags each time in order to communicate with the Docker daemon of your `manager` node.

## Clean Up the Environment

To clean up the environment, run:

```bash
docker compose down --remove-orphans -v
```
