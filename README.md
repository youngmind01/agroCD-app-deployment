# agroCD-app-deployment

Step 1.
# install ArgoCD in k8s
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

Step 2. 
Follow the instructions to configure a certificate (and ensure that the client OS trusts it).
Configure the client OS to trust the self signed certificate.
# generate a self-signed TLS certificate using OpenSSL:


# access ArgoCD UI
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# login with admin user and below token (as in documentation):
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# you can change and delete init password
