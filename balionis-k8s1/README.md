## Why?
It's a 'kind' install instructions prototype under docker desktop.

### Download
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.18.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /opt/local/bin/kind
```

## Create Cluster
```
kind create cluster --config config/kind-config.yml
```

### Test
```
export KUBECONFIG=~/.kube/config
kind get clusters
kubectl cluster-info --context kind-kind
kind export logs
```

### Test
```
kind delete cluster
```

## List/Load images
```
docker exec -it kind-control-plane crictl images

kind load docker-image my-custom-image:unique-tag 
```

## Deploy Sample service
```
kubectl apply -f ./config/nginx-deployment.yml
kubectl apply -f ./config/nginx-service.yml

kubectl port-forward service/nginx-service 8080:8080 

curl http://localhost:8080
```

## Ingress (NGINX)

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
  
kubectl apply -f ./config/nginx-ingress.yml

curl --insecure https://localhost

```
