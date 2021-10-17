# How to enable eBPF for Calico
```
kubectl apply -f kubernetesServicesEndpoint.yaml
kubectl delete pod -n kube-system -l k8s-app=calico-node
kubectl delete pod -n kube-system -l k8s-app=calico-kube-controllers
kubectl patch ds -n kube-system kube-proxy -p '{"spec":{"template":{"spec":{"nodeSelector":{"non-calico": "true"}}}}}'
kubectl calico patch felixconfiguration default --patch='{"spec": {"bpfKubeProxyIptablesCleanupEnabled": false}}'
kubectl patch felixconfiguration default --patch='{"spec": {"bpfEnabled": true}}'
```

# How to disable eBPF for Calico
```
kubectl calico patch felixconfiguration default --patch='{"spec": {"bpfEnabled": false}}'
```
