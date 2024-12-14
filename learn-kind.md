# Setup kind to run nginx

1. Set **kubectl** context to "kind-kind" `kubectl cluster-info --context kind-kind`

2. Check information about this

   ```bash
   ❯ kubectl cluster-info --context kind-kind
   Kubernetes control plane is running at https://127.0.0.1:49369
   CoreDNS is running at https://127.0.0.1:49369/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
   ```

3. Above I installed docker so here is a query on docker for seeing this

   ```bash
   ❯  docker exec -it kind-control-plane crictl images
   registry.k8s.io/etcd                            3.5.15-0             27e3830e14027       66.5MB
   registry.k8s.io/kube-apiserver-arm64            v1.31.2              7db5e8fdce19a       92.6MB
   registry.k8s.io/kube-apiserver                  v1.31.2              7db5e8fdce19a       92.6MB
   registry.k8s.io/kube-controller-manager-arm64   v1.31.2              d034a1438c8ae       87MB
   registry.k8s.io/kube-controller-manager         v1.31.2              d034a1438c8ae       87MB
   registry.k8s.io/kube-proxy-arm64                v1.31.2              7e641dea6ec8f       96MB
   registry.k8s.io/kube-proxy                      v1.31.2              7e641dea6ec8f       96MB
   registry.k8s.io/kube-scheduler-arm64            v1.31.2              4ff74b8997ace       67MB
   registry.k8s.io/kube-scheduler                  v1.31.2              4ff74b8997ace       67MB
   registry.k8s.io/pause                           3.10                 afb61768ce381       268kB
   ```

4. In the repository is a [deployment.yaml](./deployment.yaml) file to deploy an nginx load balancer

   ```bash
   ❯ kubectl apply -f deployment.yaml
   deployment.apps/nginx-deployment created
   ```

5. **Check** if it is up and running

   ```bash
   ❯ kubectl get pods
   NAME                                READY   STATUS    RESTARTS   AGE
   nginx-deployment-54b9c68f67-h4sxh   1/1     Running   0          83s
   nginx-deployment-54b9c68f67-p6jdv   1/1     Running   0          83s
   nginx-deployment-54b9c68f67-t28t6   1/1     Running   0          83s
   ```

6. Set this up with **port forwarding** ...

   ```bash
   ❯ kubectl port-forward nginx-deployment-54b9c68f67-h4sxh 8000:80
   Forwarding from 127.0.0.1:8000 -> 80
   Forwarding from [::1]:8000 -> 80
   ```

7. **Browse** to this and remember as soon as you close that session, port forwading will dissapear

   ![Port forwarded browser](/Users/Vincent.Farah/Dev/localkubekindexercise/assets/nginx-in-browser.png)

8. **Query** the pods

   ```bash
   ❯ kubectl get pods
   NAME                                READY   STATUS    RESTARTS   AGE
   nginx-deployment-54b9c68f67-h4sxh   1/1     Running   0          83s
   nginx-deployment-54b9c68f67-p6jdv   1/1     Running   0          83s
   nginx-deployment-54b9c68f67-t28t6   1/1     Running   0          83s
   ```

9. **Scale up** replicas to 5 and redeploy within the local **deployment.yaml** file changing `replicas: 3` to `replicas: 5` 

   ```
   ❯ kubectl apply -f deployment.yaml
   	deployment.apps/nginx-deployment configured
   
   ❯ kubectl get pods
   
     NAME                                READY   STATUS    RESTARTS   AGE
   	nginx-deployment-54b9c68f67-7lfn8   1/1     Running   0          6s
   	nginx-deployment-54b9c68f67-h4sxh   1/1     Running   0          46h
   	nginx-deployment-54b9c68f67-p6jdv   1/1     Running   0          46h
   	nginx-deployment-54b9c68f67-rlvw4   1/1     Running   0          6s
   	nginx-deployment-54b9c68f67-t28t6   1/1     Running   0          46h
   
   ```

10. **Delete** this and cleanup

    ```bash
    ❯ kubectl delete -f deployment.yaml
    deployment.apps "nginx-deployment" deleted
    ```

11. **Check** there are no pods

    ```bash
    ❯ kubectl get pods
    No resources found in default namespace.
    ```

### 