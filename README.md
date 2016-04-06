Vagrant Jenkins Tests
=====================

### Installation

You will need [Vagrant](https://www.vagrantup.com) and [Virtualbox](https://www.virtualbox.org/) installed on your system.
Also you will need to clone this repository and get all the roles:
```sh
git clone https://github.com/amatas/vagrant-jenkins-test
cd vagrant-jenkins-test
ansible-galaxy install -r requirements.yml -p provisioning/roles/
```

_The Vagranfile is also compatible with [vagrant-libvirt](https://github.com/pradels/vagrant-libvirt)_

### Steps recreated on this environment

By default the [Vagrantfile] will create 3 VMs, one master and two slaves. Each VM will use 1G of RAM, so at least 3G of free ram is required.

The following steps are performed when the VMs are provisioned:

On master:

1. Setup Jenkins master service ([ansible-jenkins-master](https://github.com/amatas/ansible-jenkins-master))
1. Configure Jenkins' users ([ansible-jenkins-master](https://github.com/amatas/ansible-jenkins-master))
1. Configure Jenkins' credentials ([ansible-jenkins-master](https://github.com/amatas/ansible-jenkins-master))
1. Download and install plugins ([ansible-jenkins-master](https://github.com/amatas/ansible-jenkins-master))
1. Install Jenkins-job-builder and configure the API user ([ansible-jenkins-master](https://github.com/amatas/ansible-jenkins-master))
1. Install a reverse proxy _http://10.0.0.10/_ ([ansible-nginx-reverse](https://github.com/idi-ops/ansible-nginx-reverse))
1. Install docker-registry ([ansible-docker-registry](https://github.com/amatas/ansible-docker-registry))
1. Register a [Jenkins job](provisioning/test-jobs/docker.yml)

On slaves:

1. Setup Jenkins node and register at the server
1. Install docker daemon ([ansible-docker](https://github.com/idi-ops/ansible-docker))
1. Install certificates to stablis TLS connection to the docker-registry

After provision you can access to the Jenkins Dashboard (u: admin, p: root) and trigger the build.

