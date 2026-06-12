# Kubernetes-gaming
Déploiement de jeux sur kubernetes
# Kubernetes Gaming — Tetris sur Kubernetes

## Description
Déploiement d'un jeu vidéo (Tetris) sur Kubernetes pour démontrer les concepts d'auto-healing et de scaling automatique.

## Technologies utilisées
- Kubernetes (Minikube)
- Docker
- kubectl

## Architecture
- 1 Deployment Tetris
- 1 Service NodePort (port 30080)
- Auto-healing activé

## Installation

### Prérequis
- Docker installé
- Minikube installé
- kubectl installé

### Lancer le projet
```bash
minikube start
minikube image load bsord/tetris
kubectl apply -f deployment.yaml
minikube service tetris --url
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

## Cas d'usage réel
- Fortnite (Epic Games)
- Pokémon GO (Google + Niantic)
- Riot Games (League of Legends)
