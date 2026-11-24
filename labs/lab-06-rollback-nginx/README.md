# Lab 06 — Rollback d'un Deployment nginx

## 🎯 Consigne

Une release boguée a été déployée : revenir à la révision précédente du Deployment `nginx-deployment`.

## 🛠️ Résolution

```bash
# 1. État avant
kubectl rollout history deployment/nginx-deployment
kubectl get deployment nginx-deployment -o jsonpath='{.spec.template.spec.containers[0].image}{"\n"}'

# 2. Rollback
kubectl rollout undo deployment/nginx-deployment

# 3. Suivre
kubectl rollout status deployment/nginx-deployment

# 4. Vérifier
kubectl get deployment nginx-deployment -o jsonpath='{.spec.template.spec.containers[0].image}{"\n"}'
kubectl get pods
kubectl get rs                       # l'ancien RS a repris les pods
kubectl rollout history deployment/nginx-deployment
```

## 💡 Ce que j'ai retenu

- `rollout undo` = un rolling update à l'envers, toujours sans coupure
- La révision restaurée change de numéro (1 → 3) : deux `undo` d'affilée font un aller-retour
- Pour viser une version précise : `--to-revision=N`
- Fiche associée : [Rollback](../../fiches/06-rollback.md) (complète [Rolling update](../../fiches/05-rolling-update.md))
