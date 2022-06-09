# Env setup

# gcp version

I followed this tutorial to create the virtual machines on gcp:

https://docs.ansible.com/ansible/latest/scenario_guides/guide_gce.html

Below the main steps:

1. pip install requests google-auth
2. install gcloud compute regions list
3. create a service account on you project
4. download the key 
5. [TODO] add the key to github secret
5. create an ssh-key and add it on GCP (Compute Engine->Settings->Metadata)

# ansible requirement

1. ansible-galaxy install -r requirements.yml


# vagrant version
1. install vagrant