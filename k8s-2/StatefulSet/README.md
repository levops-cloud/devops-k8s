mk apply -f web.yaml
 mk get service nginx
 mk get statefulset
 mk get pod

For a StatefulSet with N replicas, when Pods are being deployed, they are created sequentially, in order from {0..N-1}. Examine the output of the kubectl get command in the first terminal. Eventually, the output will look like the example below.

Pods in a StatefulSet have a unique ordinal index and a stable network identity.
for i in 0 1; do microk8s.kubectl exec web-$i -- sh -c 'hostname'; done
microk8s.kubectl run -i --tty --image busybox:1.28 dns-test --restart=Never --rm  nslookup web-0.nginx
microk8s.kubectl run -i --tty --image busybox:1.28 dns-test --restart=Never --rm  nslookup web-1.nginx

microk8s.kubectl get pvc

microk8s.kubectl scale sts web --replicas=5

--- 
microk8s.kubectl delete sts web
microk8s.kubectl delete sts web --cascade=false
