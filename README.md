# Deploy beats to ECS nodes

Deploy filebeat on ECS nodes to forward access logs to kafka.

# Setup
1. Install [Docker](http://docker.io)
2. Install [Ansible](http://docs.ansible.com/ansible/intro_installation.html)
3. Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
4. Clone this repository


# Deploy beats to ECS nodes
Deploy filebeat on ECS nodes. The filebeat is configured to collect access log from dataheadsvc.log and forward to kafka.

Make sure ECS nodes can be accessed via ssh, and the nodes themselves can access kafka port (9092 by default).

Edit work/inventory to specify ECS nodes, vdc, and output_kafka_hosts

Execute the following commands to download docker images and deploy containers on ECS nodes

```bash
$ ansible-playbook ssh-key.yml --ask-pass
$ sudo ansible-playbook upload-image.yml
$ ansible-playbook install.yml
```

Log on to an ECS node to verify filebeat and metricbeat containers are running. 
```bash
$ sudo docker logs filebeat
```

You will need to create a topick called "ecs-accesslog". You can start a kafka consumer to listent to the topic to verify the data. 
