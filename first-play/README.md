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

## flow control

```sh
# https://helm.sh/docs/chart_template_guide/control_structures/
#  通过类似如下方式达到激活helm配置或者不激活的效果
#   {{ if PIPELINE }}
  # Do something
#   {{ else if OTHER PIPELINE }}
  # Do something else
#   {{ else }}
  # Default case
#   {{ end }}


{{- with .Values.imagePullSecret }}
apiVersion: v1
kind: Secret
type: kubernetes.io/dockerconfigjson
metadata:
  name: {{ .name }}
data:
  .dockerconfigjson: {{ template "imagePullSecret" . }}
{{- end }}
```

```sh
# create helm chart via template-values
helm3 --kubeconfig=/home/marco/kubeconfig install sample-application ./sample-application-helm --set=imagePullSecret.username=test,imagePullSecret.password=testpwd,ingress.host=sample-application.ingress.cluster.gprojectname.cluster.k8s.cn --wait
```
