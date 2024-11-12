# Procedure to pull and run OAI 5G core docker images 


```bash
cd ieee_ants2024_oai_tutorial/cn
```

If you do not have a docker account, create a docker account in [docker signup](https://www.docker.com/) 

Login to docker

```bash
docker login -u <username>
```

Enter your password

Now, pull the 5G core docker images

```bash
sudo docker compose pull
```

start core network
```bash
sudo docker compose -f docker-compose.yml up -d
```

sudo watch status of the core network
```bash
sudo watch docker compose -f docker-compose.yml ps -a
```
All the docker containers should be `healthy`
