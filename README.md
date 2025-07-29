GitOps with ArgoCD - Complete Setup Guide

Official Documentation:
https://argo-cd.readthedocs.io/en/stable/getting_started/

1. INSTALLATION
Command:
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
Image: https://github.com/user-attachments/assets/97ad22ee-2a5f-4d49-ac19-41602439007e

2. MONITORING POD CREATION
Command:
kubectl get pods -n argocd -w
Image: https://github.com/user-attachments/assets/53abd950-5854-4a89-b6d1-3c2caf8093e6

3. CHECKING SERVICES
Command:
kubectl get svc -n argocd
Image: https://github.com/user-attachments/assets/8a80893d-993a-4db6-9eba-53440b4fe93d

4. EXPOSING ARGOCD SERVER
Command:
kubectl edit svc argocd-server -n argocd
(Change ClusterIP to NodePort)
Image 1: https://github.com/user-attachments/assets/d02322c6-528c-42ad-a1c6-79ca02a9d557
Image 2: https://github.com/user-attachments/assets/a68b6ffe-883f-4aad-a51e-4e3a80a7827b

5. VERIFYING SERVICE CHANGES
Command:
kubectl get svc -n argocd -o wide
Image: https://github.com/user-attachments/assets/3f29250d-64ad-40c2-b459-19729f636836
UI Access URL shown in image: https://github.com/user-attachments/assets/e1352639-7a60-4a46-ad4b-f96836363e16

6. RETRIEVING LOGIN CREDENTIALS
Command:
kubectl get secret -n argocd
Image: https://github.com/user-attachments/assets/56e3d7b2-193c-438f-9d68-687bf2ec8418

Command:
kubectl edit secret argocd-initial-admin-secret -n argocd
Image: https://github.com/user-attachments/assets/bfcfb18f-18f4-4da9-9d32-50cdf334089d

Decoding Password:
echo password== | base64 --decode
Example:
echo OGFWSURuSWNvcTJzMW40Mw== | base64 --decode

Login Credentials:
Username: admin
Password: [your decoded password]

Login Screen: https://github.com/user-attachments/assets/d4cc2450-a20b-4916-ae9a-eb287e906927
Dashboard: https://github.com/user-attachments/assets/ddfb4cbe-7562-4c6e-a185-c1f57e8c1bba

7. SETTING UP CD PIPELINE
Example Repository:
https://github.com/argoproj/argocd-example-apps/tree/master/guestbook
(Note: HEAD is configured to automatically track the latest commit)

Setup Images:
1. https://github.com/user-attachments/assets/95f27cc3-c8a1-484b-a98f-70a8e1e19ad0
2. https://github.com/user-attachments/assets/60fe800a-5e91-4579-b42b-fbe35d52ee56
3. https://github.com/user-attachments/assets/46a2a6f1-1770-4e02-8204-4ce7d9e624a7
4. https://github.com/user-attachments/assets/e042bd55-b0ee-4820-8275-09808768355f

8. DEPLOYMENT RESULTS
Deployed Application: https://github.com/user-attachments/assets/79e56221-3a44-4e8d-ab99-b96e01b06c4b
Resource View: https://github.com/user-attachments/assets/0d06b58a-3725-4ac3-93c2-429dae3d7f54

9. CLI VERIFICATION
Command:
kubectl get pods
Image: https://github.com/user-attachments/assets/6149ec48-076b-45dc-b966-e7a093226ff6

10. ACCESSING GUESTBOOK
Command:
kubectl port-forward svc/guestbook-ui 8080:80
Image 1: https://github.com/user-attachments/assets/ef8b2af3-45bf-4bd9-8d7b-66f696e95726
Image 2: https://github.com/user-attachments/assets/87ff47d0-dd0a-47d2-8e5d-76a55b3406b1
