# Kubernetes Gaming — Tetris sur Kubernetes

## Description
Déploiement d'un jeu vidéo (Tetris) sur Kubernetes pour démontrer les concepts 
d'auto-healing, de scaling automatique et de gestion avec Helm.

## Technologies utilisées
- Kubernetes (Minikube)
- Docker
- kubectl
- **Helm v3** (gestionnaire de paquets Kubernetes)

## Architecture
- 1 Deployment Tetris (via kubectl)
- 1 Helm chart (tetris-chart/)
- 1 Service NodePort (port 30080 / 30090)
- Auto-healing activé
- Scaling jusqu'à 3 replicas

## Installation

### Prérequis
- Docker installé
- Minikube installé
- kubectl installé
- Helm v3 installé

### Installer Helm
```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm version
```

### Lancer le projet avec kubectl
```bash
minikube start
minikube image load bsord/tetris
kubectl apply -f deployment.yaml
minikube service tetris --url
```

### Lancer le projet avec Helm
```bash
minikube start
minikube image load bsord/tetris
helm install tetris-helm ./tetris-chart
helm list
kubectl get pods
```

## Démonstration auto-healing
```bash
kubectl delete pod -l app=tetris
kubectl get pods -w
```
Le pod redémarre automatiquement en moins de 5 secondes.

## Démonstration scaling
```bash
kubectl scale deployment tetris --replicas=3
kubectl get pods
```

## Gestion avec Helm
```bash
# Voir les releases
helm list

# Mettre à jour
helm upgrade tetris-helm ./tetris-chart

# Rollback
helm rollback tetris-helm 1

# Historique
helm history tetris-helm

# Désinstaller
helm uninstall tetris-helm
```

## Structure du projet
