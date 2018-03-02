Instrukcje:

1. Utworzenie klastra na aws:

* Przygotowania do utworzenia klastra na AWS:
    * Należy przygotować użytkownika IAM
    * Bucket na S3
    * Domenę
    * Hosted zone w Route 53

* Utworzenie przy pomocy KOPS:

```
kops create cluster --name=wilqmwb.tk --state=s3://kops-state-wilqmwb --zones=eu-central-1a --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=wilqmwb.tk

kops update cluster wilqmwb.tk --yes --state=s3://kops-state-wilqmwb
```

Utworzenie dashboardu:

```
kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/kubernetes-dashboard/v1.5.0.yaml
```

https://api.wilqmwb.tk/ui

user: admin
password: z kubectl config view --minify

Utworzenie pozostałych elementów:

```
kubectl create -f manifests/frontend_deployment.yml

kubectl create -f manifests/frontend_loadbalancer.yml

kubectl create -f manifests/secrets.yml

kubectl create -f manifests/backend_deployment.yml

kubectl create -f manifests/backend_loadbalancer.yml
```



