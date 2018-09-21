# planescape_docker

Dockerfile repository for maintaining Planescape MUD Docker images.

## Local: Planescape MUD instance for development

Steps you need to build it locally:

* Clone this repository
```bash
git clone https://github.com/planescape-mud/planescape_docker.git
cd local
```

* Build and launch the container, exposing port 4000 to the host. 
  Logs are in /home/planescape/runtime/var/log.
```bash
docker build -t planescape/local .
docker run --name planescape -p 4000:4000 -it planescape/local
```

* Connect to the game:
```bash
telnet localhost 4000
```

Later on, if you want to get a shell access to the running container:
```bash
docker exec -it planescape /bin/bash
```

To restart a stopped container and continue your work:
```bash
docker restart planescape
```

To copy files from your local box to the container, use:
```bash
docker cp yourfile.cpp planescape:/home/planescape/planescape_code/src
```

See [main project's Readme](https://github.com/planescape-mud/planescape_code/blob/master/README.md) on how to rebuild and restart the server or one of its plugins.

