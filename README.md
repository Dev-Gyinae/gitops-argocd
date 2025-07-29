# GitOps with ArgoCD - Complete Setup Guide

Official guide: https://argo-cd.readthedocs.io/en/stable/getting_started/

## Installation and Setup

1. Install ArgoCD:
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
![Installation](https://github.com/user-attachments/assets/97ad22ee-2a5f-4d49-ac19-41602439007e)

2. Monitor pod creation:
kubectl get pods -n argocd -w
![Pod Status](https://github.com/user-attachments/assets/53abd950-5854-4a89-b6d1-3c2caf8093e6)

3. Check services:
kubectl get svc -n argocd
![Services](https://github.com/user-attachments/assets/8a80893d-993a-4db6-9eba-53440b4fe93d)

4. Change service type to NodePort:
kubectl edit svc argocd-server -n argocd
Change type from ClusterIP to NodePort
![Service Edit](https://github.com/user-attachments/assets/d02322c6-528c-42ad-a1c6-79ca02a9d557)
![NodePort](https://github.com/user-attachments/assets/a68b6ffe-883f-4aad-a51e-4e3a80a7827b)

5. Verify changes:
kubectl get svc -n argocd -o wide
![Service Details](https://github.com/user-attachments/assets/3f29250d-64ad-40c2-b459-19729f636836)

UI Access:
![UI Address](https://github.com/user-attachments/assets/e1352639-7a60-4a46-ad4b-f96836363e16)

## Accessing ArgoCD

1. Get login credentials:
kubectl get secret -n argocd
![Secrets](https://github.com/user-attachments/assets/56e3d7b2-193c-438f-9d68-687bf2ec8418)

2. Decode password:
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode
Example: echo OGFWSURuSWNvcTJzMW40Mw== | base64 --decode
![Secret Details](https://github.com/user-attachments/assets/bfcfb18f-18f4-4da9-9d32-50cdf334089d)

Login with:
Username: admin
Password: [your decoded password]
![Login](https://github.com/user-attachments/assets/d4cc2450-a20b-4916-ae9a-eb287e906927)
![Dashboard](https://github.com/user-attachments/assets/ddfb4cbe-7562-4c6e-a185-c1f57e8c1bba)

## Setting Up CD Pipeline

Example repo: https://github.com/argoproj/argocd-example-apps/tree/master/guestbook
(Note: HEAD is set to automatically track latest commit)

Application setup screens:
![App Setup 1](https://github.com/user-attachments/assets/95f27cc3-c8a1-484b-a98f-70a8e1e19ad0)
![App Setup 2](https://github.com/user-attachments/assets/60fe800a-5e91-4579-b42b-fbe35d52ee56)
![App Setup 3](https://github.com/user-attachments/assets/46a2a6f1-1770-4e02-8204-4ce7d9e624a7)
![App Setup 4](https://github.com/user-attachments/assets/e042bd55-b0ee-4820-8275-09808768355f)

Deployed application:
![Deployed App](https://github.com/user-attachments/assets/79e56221-3a44-4e8d-ab99-b96e01b06c4b)

Resource view:
![Resource View](https://github.com/user-attachments/assets/0d06b58a-3725-4ac3-93c2-429dae3d7f54)

CLI verification:
kubectl get pods
![CLI Verification](https://github.com/user-attachments/assets/6149ec48-076b-45dc-b966-e7a093226ff6)

Accessing guestbook:
kubectl port-forward svc/guestbook-ui 8080:80
![Port Forward](https://github.com/user-attachments/assets/ef8b2af3-45bf-4bd9-8d7b-66f696e95726)
![Guestbook UI](https://github.com/user-attachments/assets/87ff47d0-dd0a-47d2-8e5d-76a55b3406b1)
