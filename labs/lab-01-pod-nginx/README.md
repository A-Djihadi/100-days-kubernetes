# Lab 01 — Créer un Pod nginx

## 🎯 Consigne

- Créer un pod `pod-nginx` avec l'image `nginx:latest`
- Label `app=nginx_app`
- Container nommé `nginx-container`

## ⚠️ Le piège

`kubectl run` nomme le container comme le pod et ne propose aucune option pour le changer.
→ Il faut passer par un **manifest YAML**.

## 🛠️ Résolution

```bash
# 1. Générer un squelette (rien n'est créé dans le cluster)
kubectl run pod-nginx --image=nginx:latest --labels=app=nginx_app \
  --dry-run=client -o yaml > pod-nginx.yaml

# 2. Renommer le container en nginx-container (cf. pod-nginx.yaml)

# 3. Appliquer
kubectl apply -f pod-nginx.yaml

# 4. Vérifier
kubectl get pod pod-nginx --show-labels
kubectl get pod pod-nginx -o jsonpath='{.spec.containers[0].name} {.spec.containers[0].image}{"\n"}'
```

## 💡 Ce que j'ai retenu

- `--dry-run=client -o yaml` : le meilleur réflexe pour générer un YAML sans le taper à la main
- Le tag explicite (`:latest`) évite les ambiguïtés, mais en prod on épingle une version précise
- Fiche associée : [Pod](../../fiches/01-pod.md)
