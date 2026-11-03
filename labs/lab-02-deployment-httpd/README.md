# Lab 02 — Créer un Deployment httpd

## 🎯 Consigne

Créer un Deployment `httpd` avec l'image `httpd:latest` (tag explicite).

## 🛠️ Résolution

```bash
# Impératif (une ligne)
kubectl create deployment httpd --image=httpd:latest

# Ou déclaratif
kubectl apply -f deployment-httpd.yaml

# Vérifier
kubectl get deployment httpd
kubectl get rs,pods -l app=httpd
kubectl get deployment httpd -o jsonpath='{.spec.template.spec.containers[0].image}{"\n"}'
```

## 💡 Ce que j'ai retenu

- 1 objet créé → 3 objets dans le cluster : **Deployment → ReplicaSet → Pod**
- Supprimer le pod ne sert à rien : le ReplicaSet le recrée (auto-réparation)
- `selector.matchLabels` doit correspondre aux labels du `template` : c'est le lien entre les niveaux
- Fiche associée : [Deployment](../../fiches/02-deployment.md)
