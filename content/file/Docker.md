#self-taught 
`docker system prune --force` should delete stupidly big files popping out of god-damn-nowhere.

disk image location: `/Users/davidesqueri/Library/Containers/com.docker.docker/Data/vms/0/data`

qui c'è docker.raw che è enorme e contiene tipo tutto quello che serve a docker, era 1.1tb poi ho ridotto la disk size di docker da 1tb a 8gb e adesso è 34gb, ma 0gb on disk.: `/Users/davidesqueri/Library/Containers/com.docker.docker/Data/vms/0/data`

Le immagini costruite vengono salvate qua su macos:
`~/Library/Containers/com.docker.docker/Data/vms/0/`
Nota: non c’è una cartella “linux-x86-env” visibile nel filesystem — Docker gestisce tutto dentro un’immagine virtuale (una specie di disco interno del suo ambiente Linux).

Puoi visualizzare dove e quanto spazio occupano le immagini docker con:
`docker system df`

```shell
docker volume ls
docker volume inspect volumeName
"CreatedAt": "2025-10-19T15:34:06+02:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/vscode/_data",
        "Name": "vscode",
        "Options": null,
        "Scope": "local"
        
docker system df
docker image ls
REPOSITORY       TAG       IMAGE ID       CREATED         SIZE
myapp            latest    a1b2c3d4e5f6   2 days ago      300MB
ubuntu           latest    123456789abc   3 weeks ago     77MB        
# docker images instead are stored inside VM (/var/lib/docker)
```
### delete images, containers, volumes
```bash
# Use the IMAGE ID or repository:tag
docker rmi imageID
docker rmi -f ...
docker rmi myapp:latest

# to delete every image:
docker rmi -f $(docker images -q)

# to delete docker unused data:
docker system prune -a

# to delete volume
docker volume rm nome
# to delute unused volumes
docker volume prune

docker container ls -a
docker container rm nome
```
### docker run
```shell
man docker-run

docker run -v hostDir:containerDir
```
### docker build
```shell
man docker-build

docker build PATH | URL | -

docker build -t tagDaDare
```
# Docker Desktop
Disk image location:
/Users/davidesqueri/Library/Containers/com.docker.docker/Data/vms/0/data
# Colima
On macOS docker must run inside a linux VM, the preferred method is to use Colima, which will be the docker Daemon.
```shell
brew install colima
colima version
colima status
colima start --auto-start
colima start
colima stop
colima delete # deletes current configuration and settings, must be run to reduce disk size

colima ssh # connect to vm

# permanent resource limits for colima
colima start --cpu 4 --memory 8 --disk 20

docker info | grep -E 'CPUs|Memory'

# for persistent, versioned settings, create or edit:
~/.colima/default/colima.yaml

colima delete
rm -rf ~/.colima
```

colina.yaml:
for persistent, versioned settings, create or edit:
`~/.colima/default/colima.yaml`
```yaml
cpu: 4
memory: 8
disk: 20 # GB
vmType: vz  # 'vz' = Apple Virtualization Framework (best for M1/M2/M3)
arch: aarch64
docker:
  runtime: containerd
```