# agroCD-app-deployment

Step 1.
# install ArgoCD in k8s
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

Step 2. 
Follow the instructions to configure a certificate (and ensure that the client OS trusts it).
Configure the client OS to trust the self signed certificate.
# ----generate a self-signed TLS certificate using OpenSSL:
![Screenshot from 2023-05-04 02-37-06](https://user-images.githubusercontent.com/54754559/236090422-4a5d95e8-75f4-456e-afde-7f5e4e993110.png)
This command will generate a self-signed TLS certificate with a validity of 365 days, using a key size of 2048 bits. The -subj option specifies the subject of the certificate, which should match the hostname or IP address of your ArgoCD server.

# ----Create a Kubernetes secret to store the TLS certificate:
![Screenshot from 2023-05-04 02-41-34](https://user-images.githubusercontent.com/54754559/236090739-d10602bf-2010-4d7e-9814-437999f8f198.png)
This command will create a secret named argocd-server-tls in the argocd namespace, containing the TLS certificate and key.

# ----Modify the ArgoCD server deployment to use the TLS certificate:
![Screenshot from 2023-05-04 02-49-36](https://user-images.githubusercontent.com/54754559/236091582-89fa70f4-43f6-4e12-a638-6db2d94e71d0.png)
This command will modify the argocd-server deployment to mount the argocd-server-tls secret as a volume, and configure the ArgoCD server container to use the TLS certificate and key.

# ----Verify that the ArgoCD server is now using TLS by checking the logs of the argocd-server container:
![Screenshot from 2023-05-04 02-51-05](https://user-images.githubusercontent.com/54754559/236091884-4bad62e1-2d61-4b0e-9618-af11d3d078f9.png)
This command should output a message indicating that the HTTPS server has started, indicating that the ArgoCD server is now using TLS.

By following these steps, you should now have configured your Kubernetes cluster to trust the ArgoCD server's TLS certificate.

# access ArgoCD UI
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# login with admin user and below token (as in documentation):
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# you can change and delete init password
