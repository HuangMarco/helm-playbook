# first play

## resources

```sh
# create namespace
kubectl create ns test
# create deployment nginx using the latest image
kubectl create deployment nginx --image=nginx -n test
# get the k8s deployment and export to the local
kubectl get deployment nginx -n test -o yaml > deployment-nginx.yaml
# modify the deployment-nginx to add the port information

# ports:
# - containerPort: 80
#   protocol: TCP

kubectl delete deployment nginx -n test
kubectl apply -f deployment-nginx.yaml

# expose the deployment:nginx to the service
kubectl expose deployment/nginx -n test




# 上面命令等效于下面：
kubectl run nginx --image=nginx:1.13.5-alpine\
-o yaml > deployment-nginx.yaml

kubectl expose deployment nginx -n test --port=81 --type=NodePort \
-o yaml > service-81.yaml
```
