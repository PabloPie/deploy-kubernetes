# Bootstrap a Caliopen instance on a Kubernetes cluster on Gandi IaaS platform

## Requirements:

* Libcloud with Gandi module
* Ansible with Gandi modules and dynamic inventory script
* Gandi IaaS account and its api key

---

## Bootstraping the cluster:

1. Configure the VM deployment modifying the file ```vm_vars/settings.yaml```
2. Set your Gandi IaaS API key modifying the file ```vm_vars/credentials.yaml```
3. Create the VMs
	* ``` ansible-playbook vm-deploy.yml```
4. Configure your deployment modifying the file ```group_vars/all```
5. Setup your k8s cluster and deploy Caliopen on it
	* ``` ansible-playbook -i PATH_TO_DYNAMIC_INVENTORY_SCRIPT deployment.yml```
6. From your master node, setup the storage with
	* ```kubectl create -f https://raw.githubusercontent.com/PabloPie/deploy-kubernetes/master/jobs/cli-setup.yaml```


---

## Options:

### SMTP Server:

For now the cluster must be deployed with an external SMTP server. Set your smtp server's ip address in the file ```group_vars/all```.

### Storage:

* The cluster supports in-cluster storage with local storage, needing one disk per node per application, to use this option set the variable external-storage in ```group_vars/all``` to false.
* You can also use your own Cassandra/Minio/Elasticsearch cluster, for this you need to set the external-storage variable to true, the deployment will create services with external endpoints. Set your storage servers' ip addresses in the file ```group_vars/all```.
