# Lab 05 — Rolling update d'un Deployment nginx

## 🎯 Consigne

Mettre à jour le Deployment existant `nginx-deployment` vers l'image `nginx:1.17` via un rolling update, et vérifier que tous les pods tournent.

## ⚠️ Le piège

`kubectl set image` exige le **nom du container**, absent de la consigne → l'inspecter d'abord (ou utiliser `*`).

## 🛠️ Résolution

```bash
# 1. Inspecter
kubectl get deployment nginx-deployment -o wide
kubectl get deployment nginx-deployment -o jsonpath='{.spec.template.spec.containers[*].name}{"\n"}'

# 2. Rolling update
kubectl set image deployment/nginx-deployment <container>=nginx:1.17
#   ou, tous les containers : kubectl set image deployment/nginx-deployment '*=nginx:1.17'

# 3. Suivre
kubectl rollout status deployment/nginx-deployment

# 4. Vérifier
kubectl get pods
kubectl get rs                       # nouveau RS = N pods, ancien RS = 0
kubectl rollout history deployment/nginx-deployment

# En cas de souci
kubectl rollout undo deployment/nginx-deployment
```

## 💡 Ce que j'ai retenu

- Un changement du `template` du pod (ici l'image) déclenche un nouveau ReplicaSet
- La bascule est progressive, réglée par `maxSurge` et `maxUnavailable` (25 % par défaut)
- L'ancien ReplicaSet est conservé à 0 réplica → rollback instantané
- Fiche associée : [Rolling update & rollback](../../fiches/05-rolling-update.md)
