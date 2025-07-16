Create a namespace for Argo CD:

kubectl create namespace argocd
Apply the Argo CD manifest:

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
Check services in Argo CD namespace:

kubectl get svc -n argocd
Expose Argo CD server using NodePort:

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
Forward ports to access Argo CD server:

kubectl port-forward -n argocd service/argocd-server 8443:443 &

kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo


Installing Kubernetes Dashboard
Deploy Kubernetes dashboard:

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
Create a token for dashboard access:

kubectl -n kubernetes-dashboard create token admin-user
