# cnvrg installation

## Update inventory.ini

## run the playbook:

```
ansible-playbook cnvrg/cnvrg.yml -i cnvrg/inventory.ini -e clusterDomain=cnvrg.omnia.local -e nfs_server_ip=192.168.1.104 -e storage_path=/cnvrg -e server_ip=192.168.1.104 -e metallb_ip=192.168.2.150
```

## Note:

## Calico Fix for systems with multiple NICS:

```
kubectl set env daemonset/calico-node -n kube-system IP_AUTODETECTION_METHOD=can-reach=www.google.com
```

OR define the interfaces you want to use:

```
kubectl set env daemonset/calico-node -n kube-system IP_AUTODETECTION_METHOD=interface=eno12399,ens1f0
```

## If the Pods is not up restart docker:

```
systemctl restart docker
```

## Delete cnvrg and leave clean k8s:

```
helm delete -n cnvrg cnvrg
```

```
kubectl delete istiooperators.install.istio.io -n cnvrg cnvrg-istio
```

```
kubectl delete namespaces cnvrg
```
