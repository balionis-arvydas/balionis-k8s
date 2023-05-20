## Why?
It's a 'helm' install instructions prototype under docker desktop + kind.

### Download & Install Helm
```
curl -Lo ./helm.tar.gz https://get.helm.sh/helm-v3.12.0-linux-amd64.tar.gz
tar -zxvf helm-v3.12.0-linux-amd64.tar.gz
chmod +x ./linux-amd64/helm
sudo mv ./linux-amd64/helm /opt/local/bin/helm
```

## Using App 
```
cd helm-chart
helm create balionis-k8s2 
helm install balionis-k8s2 ./balionis-k8s2 -f values-overrides.yaml
```

### Testing
```
helm get values balionis-k8s2 

kubectl --namespace default port-forward service/balionis-k8s2 8080:80

curl http://localhost:8080

helm uninstall balionis-k8s2
```
