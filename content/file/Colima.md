#self-taught 
On macOS [[docker]] must run inside a linux VM, the preferred method is to use Colima, which will be the docker Daemon.
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

colima.yaml:
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