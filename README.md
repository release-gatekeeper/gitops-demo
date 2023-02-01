# gitops-demo

1. k3d cluster create --api-port 6550 -p "8081:80@loadbalancer" --agents 2
2. helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   helm repo update
   helm install -n kube-system prom prometheus-community/kube-prometheus-stack
3. install argo rollouts
```bash
kubectl create namespace argo-rollouts
kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
```
3. kubectl argo rollouts dashboard
4. port forward `argocd-server`
5. take secret from `initial-secret`

6. install argo cd
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

7. add argocd application to demo application on default namespace: https://github.com/itai-codefresh/cncf-rollouts-demo


8. install argo cd notifications
```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj-labs/argocd-notifications/release-1.0/manifests/install.yaml
```

9. add the following changes to traefik deployment
```bash
--metrics.prometheus.addServicesLabels=true
--metrics.prometheus.addrouterslabels=true
```


links:
1. argocd - https://localhost:8080/
2. rollouts - http://localhost:3100/rollout/canary-demo
3. application - http://canary.localdev.me:8081/
4. http://canary-preview.localdev.me:8081/
