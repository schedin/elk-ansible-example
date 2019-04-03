# Vagrant/Ansible example project to set up an ELK server with http input

Based on files from [ELK examples from geerlingguy/ansible-vagrant-examples](https://github.com/geerlingguy/ansible-vagrant-examples/tree/master/elk/provisioning/elk) 

Download the required Ansible Galaxy modules:

```
ansible-galaxy install -r requirements.yml
```


Set up and provision your VM:

```
vagrant up
```

Alternatively the playbook `elk_playbook.yml` can be run manually.

Logs can be sent into the server with http, for example using curl:

```
curl -d "My test log message" -X POST http://192.168.9.90:8080/
```

Surf to http://192.168.9.90:5601/ to login to Kibana. I had to create an index pattern in Kibana to be able to see the logs in a meaningful form in the Discover menu.


## Changes from geerlingguy/ansible-vagrant-examples

1. I only used one server (the ELK server)
2. I converted the server/playbook to Centos 7 (from Ubuntu 16.04)
3. I had to disable the SSL certificates for Logstach since I got an Ansible parsing error
4. I did not test the logstash_forwarder
5. I had to remove the `/etc/logstash/conf.d/14-solr.conf` file because the multiline filter plugin was not installed.
6. I added a http input plugin source
