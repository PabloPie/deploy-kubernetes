# Bootstrap a Caliopen instance on a Kubernetes cluster on Gandi IaaS platform

### Requirements:

* Libcloud with Gandi module
* Ansible with Gandi modules and dynamic inventory script
* Gandi IaaS account and its api key



## Bootstraping the cluster:

1. Configure the VM deployment modifying the file ```vm_vars/settings.yaml```
2. Set your Gandi IaaS API key modifying the file ```vm_vars/credentials.yaml```
3. Create the VMs
	* ``` ansible-playbook vm-deploy.yml```
4. Configure your deployment modifying the file ```group_vars/all```
5. Modify the Caliopen configuration found in ```roles/caliopen/templates/configs```
6. Cluster certificates can be found in ```roles/caliopen/templates/configs``` and ```roles/lb/files```
7. Setup your k8s cluster and deploy Caliopen on it
	* ``` ansible-playbook -i PATH_TO_DYNAMIC_INVENTORY_SCRIPT deployment.yml```


## Options:

### Cluster visibility

The current configuration deploys the machines in the cluster (including the master node) exclusively with private ips. External access goes through an extra machine, external to the cluster, running HAProxy. Its configuration can be found in ```roles/lb/templates/haproxy.cfg.j2```.

### SMTP Server:

For now the cluster must be deployed with an external SMTP server.

### Storage:

The cluster must be deployed with external Cassandra, Minio, and Elasticsearch clusters.

---

### Limitations:

* The cluster deployed has a single master node

* High availability of the load balancer is not handled

