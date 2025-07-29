GitOps with ArgoCD - Complete Setup Guide

Official guide: https://argo-cd.readthedocs.io/en/stable/getting_started/

=== Installation ===
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
[image: Installation](https://github.com/user-attachments/assets/97ad22ee-2a5f-4d49-ac19-41602439007e)

=== Monitoring Pods ===
kubectl get pods -n argocd -w
[image: Pod Status](https://github.com/user-attachments/assets/53abd950-5854-4a89-b6d1-3c2caf8093e6)

=== Checking Services ===
kubectl get svc -n argocd
[image: Services](https://github.com/user-attachments/assets/8a80893d-993a-4db6-9eba-53440b4fe93d)

=== Exposing ArgoCD UI ===
kubectl edit svc argocd-server -n argocd
(change ClusterIP to NodePort)
[image: Service Edit](https://github.com/user-attachments/assets/d02322c6-528c-42ad-a1c6-79ca02a9d557)
[image: NodePort](https://github.com/user-attachments/assets/a68b6ffe-883f-4aad-a51e-4e3a80a7827b)

kubectl get svc -n argocd -o wide
[image: Service Details](https://github.com/user-attachments/assets/3f29250d-64ad-40c2-b459-19729f636836)

UI Access:
[image: UI Address](https://github.com/user-attachments/assets/e1352639-7a60-4a46-ad4b-f96836363e16)

=== Getting Credentials ===
kubectl get secret -n argocd
[image: Secrets](https://github.com/user-attachments/assets/56e3d7b2-193c-438f-9d68-687bf2ec8418)

kubectl edit secret argocd-initial-admin-secret -n argocd
[image: Secret Details](https://github.com/user-attachments/assets/bfcfb18f-18f4-4da9-9d32-50cdf334089d)

Decode password:
echo password== | base64 --decode
Example: echo OGFWSURuSWNvcTJzMW40Mw== | base64 --decode

Login:
Username: admin
Password: [your decoded password]
[image: Login](https://github.com/user-attachments/assets/d4cc2450-a20b-4916-ae9a-eb287e906927)
[image: Dashboard](https://github.com/user-attachments/assets/ddfb4cbe-7562-4c6e-a185-c1f57e8c1bba)

=== Setting Up CD Pipeline ===
Example repo: https://github.com/argoproj/argocd-example-apps/tree/master/guestbook
(HEAD set to track latest commit)

[image: App Setup 1](https://github.com/user-attachments/assets/95f27cc3-c8a1-484b-a98f-70a8e1e19ad0)
[image: App Setup 2](https://github.com/user-attachments/assets/60fe800a-5e91-4579-b42b-fbe35d52ee56)
[image: App Setup 3](https://github.com/user-attachments/assets/46a2a6f1-1770-4e02-8204-4ce7d9e624a7)
[image: App Setup 4](https://github.com/user-attachments/assets/e042bd55-b0ee-4820-8275-09808768355f)

=== Deployment Results ===
[image: Deployed App](https://github.com/user-attachments/assets/79e56221-3a44-4e8d-ab99-b96e01b06c4b)
[image: Resource View](https://github.com/user-attachments/assets/0d06b58a-3725-4ac3-93c2-429dae3d7f54)

=== CLI Verification ===
kubectl get pods
[image: CLI Check](https://github.com/user-attachments/assets/6149ec48-076b-45dc-b966-e7a093226ff6)

=== Accessing Guestbook ===
kubectl port-forward svc/guestbook-ui 8080:80
[image: Port Forward](https://github.com/user-attachments/assets/ef8b2af3-45bf-4bd9-8d7b-66f696e95726)
[image: Guestbook UI](https://github.com/user-attachments/assets/87ff47d0-dd0a-47d2-8e5d-76a55b3406b1)
