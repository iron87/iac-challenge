## GCP instance provisioning

I followed this tutorial to create the virtual machines on gcp:

https://docs.ansible.com/ansible/latest/scenario_guides/guide_gce.html

Below the main steps:

1. pip install requests google-auth
2. install gcloud sdk
3. create a service account on you project
4. download the key 
5. [TODO] add the key to github secret
5. create an ssh-key and add it on GCP (Compute Engine->Settings->Metadata)

I created a custom role for this: create-vm

## Docker Installation

For this requirement I used an existing role (available on galaxy) geerlingguy.docker. The role ensures Docker is started and enabled at boot. 

## Securing Docker Api

Use the **generate-cert.sh** to generate the certificates, then copy them to the **docker-cert** dir

I tried to configure the geerlingguy.docker using the **docker_daemon_options** var but there is an issue (https://github.com/geerlingguy/ansible-role-docker/pull/348) releated to this configuration.

Then I need to create a new role **name** 



Check if it works (add an entry to /etc/hosts, in order to resolve kira-challenge.io)

```bash
docker --tls  --tlscert cert.pem --tlskey key.pem --tlsverify --tlscacert ca.pem  --host=tcp://kira-challenge.io:2376 info 

```




1. ansible-galaxy install -r requirements.yaml

