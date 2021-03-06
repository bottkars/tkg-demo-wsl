# tkg-demo from Windows using WSL ( Windows Subsystem for Linux )

## Requirements 
- all host bootstrap host requirements from [Tanzu Bootstrap Prerequisits](https://docs.vmware.com/en/VMware-Tanzu-Kubernetes-Grid/1.0/vmware-tanzu-kubernetes-grid-10/GUID-install-tkg-set-up-tkg.html#prereqs)
- docker desktop configured/started for linux containers  
- docker desktop configured with 6GB RAM
- WSL 1.x
tested with Ubuntu 18.04
![image](https://user-images.githubusercontent.com/8255007/80176135-e8f4e000-85f7-11ea-8dea-d12bd710a0d2.png)

## expose docker daemon from wsl
in order do access docker daemon tru WSL, we need to export the docker host form WSL.
to do so, we need to check
*Expose daemon on tcp://localhost:2375 without TLS*
in docker desktop settings.
![image](https://user-images.githubusercontent.com/8255007/80172825-4e43d380-85ee-11ea-92b6-2a96a0e20776.png)

From WSL we export
```bash
export DOCKER_HOST=tcp://localhost:2375
```
tkg --ui will use xdg-open to start a Browser window. 
therefore, we use powershell to start a browser. 
use the following code to create a xdg-oben script in */usr/local/bin*
```bash
sudo tee /usr/local/bin/xdg-open <<EOF
#!/bin/sh
powershell.exe -c start "'\$@'"
EOF
sudo chmod +x /usr/local/bin/xdg-open
```
start tkg init with --ui
```bash
tkg init --ui
```

this should open your default browser (tested with edge-chromium and chrome)