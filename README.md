#


## GCP instance provisioning

I followed this tutorial to create the virtual machines on gcp:

https://docs.ansible.com/ansible/latest/scenario_guides/guide_gce.html

Below the main steps:

1. pip install requests google-auth
2. install gcloud sdk
3. create a service account on you project
4. download the key.
5. create an ssh-key and add it on GCP (Compute Engine->Settings->Metadata)

I created a custom role for this: create-vm

## Docker Installation

For this requirement I used an existing role (available on galaxy) geerlingguy.docker. The role ensures Docker is started and enabled at boot. 

## Securing Docker Api

Use the `generate-cert.sh` to generate the certificates, then set the `docker_cert_local_dir` var value with the directory path.

I tried to configure the geerlingguy.docker role, using the `docker_daemon_options` var, but there is an issue (https://github.com/geerlingguy/ansible-role-docker/pull/348) releated to this configuration.

Then I needed to create a new role: `secure_docker_api` 

Check if it works (add an entry to /etc/hosts, in order to resolve kira-challenge.io) running this command:

```bash
docker --tls  --tlscert cert.pem --tlskey key.pem --tlsverify --tlscacert ca.pem  --host=tcp://kira-challenge.io:2376 info 

```

## Install Swarm

I use an existing role to install docker swarm: tosatto.docker-swarm


### Check if swarm works 
```bash
 docker --tls  --tlscert cert.pem --tlskey key.pem --tlsverify --tlscacert ca.pem  --host=tcp://kira-challenge.io:2376 service create --replicas 3 -p 80:80 --name nginx nginx
```
## Run 

```bash
ansible-galaxy install -r requirements.yml
ansible-playbook playbook.yaml
```

## Test

The check_partition role contains a molecule test. 

### Prerequisites

You need a vagrant installation on your machine. I decided to use the vagrant driver, gce driver requires a more complex configuration and anyway the role is "platform agnostic"

Then you have to install molecule, molecule-vagrant and vagrant-disksize

```bash
pip install molecule
pip install molecule-vagrant
vagrant plugin install vagrant-disksize
```

### Run test

```bash
cd roles/check_partition
molecule test
```


