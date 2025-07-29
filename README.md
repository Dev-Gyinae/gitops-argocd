# gitops-argocd

the official guide: https://argo-cd.readthedocs.io/en/stable/getting_started/

installation of argo cd:
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
<img width="264" height="108" alt="image" src="https://github.com/user-attachments/assets/97ad22ee-2a5f-4d49-ac19-41602439007e" />


Monitoring the creation of pods
kubectl get pods -n argocd -w
<img width="742" height="166" alt="image" src="https://github.com/user-attachments/assets/53abd950-5854-4a89-b6d1-3c2caf8093e6" />


Getting the services created
kubectl get svc -n argocd
<img width="1029" height="189" alt="image" src="https://github.com/user-attachments/assets/8a80893d-993a-4db6-9eba-53440b4fe93d" />


Change the ClusterIP of the argocd-server to NodePort to enable access from a browser
kubectl edit svc argocd-server -n argocd 
<img width="1312" height="708" alt="image" src="https://github.com/user-attachments/assets/d02322c6-528c-42ad-a1c6-79ca02a9d557" />
 (change ClusterIP to NodePort)
<img width="394" height="88" alt="image" src="https://github.com/user-attachments/assets/a68b6ffe-883f-4aad-a51e-4e3a80a7827b" />

Access the changes and ports
kubectl get svc -n argocd -o wide
<img width="1324" height="220" alt="image" src="https://github.com/user-attachments/assets/3f29250d-64ad-40c2-b459-19729f636836" />

The UI address:
<img width="1281" height="16" alt="image" src="https://github.com/user-attachments/assets/e1352639-7a60-4a46-ad4b-f96836363e16" />


Getting the Login Details:
kubectl get secret -n argocd
<img width="438" height="120" alt="image" src="https://github.com/user-attachments/assets/56e3d7b2-193c-438f-9d68-687bf2ec8418" />

kubectl edit secret argocd-initial-admin-secret  -n argocd
<img width="853" height="334" alt="image" src="https://github.com/user-attachments/assets/bfcfb18f-18f4-4da9-9d32-50cdf334089d" />

copy the password in base64 and decode it
echo password== | base64 --decode
eg. echo OGFWSURuSWNvcTJzMW40Mw== | base64 --decode

Username: admin
Password: (your decoded password)
<img width="1356" height="681" alt="image" src="https://github.com/user-attachments/assets/d4cc2450-a20b-4916-ae9a-eb287e906927" />
<img width="1361" height="682" alt="image" src="https://github.com/user-attachments/assets/ddfb4cbe-7562-4c6e-a185-c1f57e8c1bba" />

Setting Up a CD process
Repo Used in example (https://github.com/argoproj/argocd-example-apps/tree/master/guestbook)
ps: HEAD is set so that it automatically triggers the latest commit
<img width="1053" height="635" alt="image" src="https://github.com/user-attachments/assets/95f27cc3-c8a1-484b-a98f-70a8e1e19ad0" />
<img width="1042" height="603" alt="image" src="https://github.com/user-attachments/assets/60fe800a-5e91-4579-b42b-fbe35d52ee56" />
<img width="1028" height="607" alt="image" src="https://github.com/user-attachments/assets/46a2a6f1-1770-4e02-8204-4ce7d9e624a7" />
<img width="1033" height="571" alt="image" src="https://github.com/user-attachments/assets/e042bd55-b0ee-4820-8275-09808768355f" />


This is how it looks after the set up:
<img width="542" height="394" alt="image" src="https://github.com/user-attachments/assets/79e56221-3a44-4e8d-ab99-b96e01b06c4b" />

Expanded view: 
It shows the status of the complete project from services files to pod deployment
<img width="1297" height="625" alt="image" src="https://github.com/user-attachments/assets/0d06b58a-3725-4ac3-93c2-429dae3d7f54" />

Confirm from CLI:
<img width="536" height="70" alt="image" src="https://github.com/user-attachments/assets/6149ec48-076b-45dc-b966-e7a093226ff6" />

Access the Guestbook CLI:
<img width="725" height="228" alt="image" src="https://github.com/user-attachments/assets/ef8b2af3-45bf-4bd9-8d7b-66f696e95726" />
<img width="1362" height="676" alt="image" src="https://github.com/user-attachments/assets/87ff47d0-dd0a-47d2-8e5d-76a55b3406b1" />

