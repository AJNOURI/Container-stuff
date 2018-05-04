
### Launch Rancher container
$ docker run -d --restart=unless-stopped -p 8080:8080 rancher/server:stable

### v2
# v2
$ sudo docker run -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher

### Start 2 Virtualbox VMs with RancherOS
$ docker-machine create -d virtualbox --virtualbox-boot2docker-url https://github.com/rancher/os/releases/download/v1.3.0/rancheros.iso rancheros1
$ docker-machine create -d virtualbox --virtualbox-boot2docker-url https://github.com/rancher/os/releases/download/v1.3.0/rancheros.iso rancheros2

### Instapect the VM's IP addresses
$ docker-machine ls

### In another terminal access the first VM
$ docker-machine ssh rancheros1

### Join the host to Rancher
[docker@rancheros1 ~]$ docker run -e CATTLE_AGENT_IP="192.168.99.100"  --rm --privileged -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/rancher:/var/lib/rancher rancher/agent:v1.2.9 http://ajnouri.info:8080/v1/scripts/79407216D85A492ACF68:1514678400000:Ng2Iowt7NiWZMnTAQNnbSp3iiU

### In another terminal access the second VM
$ docker-machine ssh rancheros2

### Join the host to Rancher
[docker@rancheros2 ~]$ docker run -e CATTLE_AGENT_IP="192.168.99.101"  --rm --privileged -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/rancher:/var/lib/rancher rancher/agent:v1.2.9 http://ajnouri.info:8080/v1/scripts/79407216D85A492ACF68:1514678400000:Ng2Iowt7NiWZMnTAQNnbSp3iiU
