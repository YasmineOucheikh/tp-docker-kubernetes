Partie 1 Docker : 
Builder et tagger
	docker build -t monappyas:1.0 .

Lancement en mappant le port
	docker run -p 5000:5000 monappyas:1.0

Vérification (dans un autre terminal)
	curl http://localhost:5000




Partie 2 Kubernetes :
### Environnement
- Cluster local : Minikube


Appliquation des manifests
	kubectl apply -f pod.yaml
	kubectl apply -f deployment.yaml
	kubectl apply -f service-clusterip.yaml
	kubectl apply -f service-nodeport.yaml

Vérification de l'état des pods
	kubectl get pods

Scaler à 3 réplicas
	kubectl scale deployment monappyas --replicas=3

Vérification des services
	kubectl get services

Accéder au service depuis l'extérieur
	minikube service monappyas-nodeport

### Vérifications
- 3 pods en statut Running
- Service ClusterIP : accessible en interne sur le port 80
- Service NodePort : accessible depuis le navigateur ( page "Welcome to nginx!" )






Partie 3 Kubernetes :

Encodage des identifiants en base64 (PowerShell)
	[Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes("yasmine"))
	[Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes("yasmine123"))

Appliquation des manifests
	kubectl apply -f configmap.yaml
	kubectl apply -f secret.yaml
	kubectl apply -f pod-config.yaml
	kubectl apply -f pvc.yaml
	kubectl apply -f pod-pvc.yaml

Vérification des ressources
	kubectl get configmap
	kubectl get secret
	kubectl get pvc
	kubectl get pods

Vérification des variables d'environnement dans le pod
	kubectl exec monappyas-config-pod -- env

### Vérifications
- ConfigMap créé avec APP_PORT=5000 et ENV_NAME=production
- Secret créé avec USERNAME et PASSWORD encodés en base64
- Pod monappyas-config-pod en Running avec les variables injectées
- PVC monappyas-pvc en statut Bound
- Pod monappyas-pvc-pod en Running avec /data monté