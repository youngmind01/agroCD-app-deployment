# agroCD-app-deployment https://gitlab.com/youngmind01/foodsoft-cluster

# Step 1.
**install ArgoCD in k8s**
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# step 2. 
**Access the dashboard UI**
kubectl port-forward -n argocd svc/argocd-server 8080:443 
then hit localhost:8080 
**Login**
user = admin 
check "kubectl get secret argocd-initial-admin-secret -n argocd -o yaml" to decode the password

using this command "echo 'put password code here' | base64 --decode

# step 3
configure ArgoCD
