# K8S 

## About Playbook

SO tested:
  - AlmaLinux
  - Centos

This playbook will install ContaineD with kubernates. The CNI Network is Calico and the network is `10.254.0.0/16`.
So, for change other network `roles/create-cluster/files/calico.yaml` and change it.

## Create cluster

Run the playbook below to create the entire framework and installation of K8S
```bash
ansible-playbook -i hosts main.yml -k
```
OBS: Remember to feed the file `hosts`.

### Documentation:
  - [ContainerD](https://kubernetes.io/docs/setup/production-environment/container-runtimes/#containerd)

### About CNI Calico

```bash
curl https://docs.projectcalico.org/manifests/calico-typha.yaml -o calico.yaml
# Altere o arquivo CALICO_IPV4POOL_CIDR e coloque o 10.0.0.0/16 
# Altere o calico-typha para o numero de replicas 3 (numero de masters)
kubectl apply -f calico.yaml
```

### Documentation:
  - [Calico](https://projectcalico.docs.tigera.io/getting-started/kubernetes/self-managed-onprem/onpremises#install-calico-with-kubernetes-api-datastore-more-than-50-nodes)

# Create a new master

To add a new master node you will need to edit the file **hosts**, leaving the session **k8s-master-shadow** just with the IP/hostname you want to add.
Now run de command:
```bash
ansible-playbook -i hosts -k new-master.yaml 
```

# Create a new worker

To add a new master node you will need to edit the file **hosts**, leaving the session **k8s-workers** just with the IP/hostname you want to add.
Now run de command:
```bash
ansible-playbook -i hosts -k new-worker.yaml
```
