# Lab 03 — Namespace dev et pod nginx

## 🎯 Consigne

- Créer le namespace `dev`
- Y déployer le pod `dev-nginx-pod` avec l'image `nginx:latest`

## 🛠️ Résolution

```bash
# Impératif
kubectl create namespace dev
kubectl run dev-nginx-pod --image=nginx:latest -n dev

# Ou déclaratif (namespace + pod dans un seul fichier, séparés par ---)
kubectl apply -f namespace-dev.yaml

# Vérifier
kubectl get ns dev
kubectl get pod dev-nginx-pod -n dev -o wide
```

## 💡 Ce que j'ai retenu

- Sans `-n`, kubectl travaille dans `default` : `kubectl get pod dev-nginx-pod` → NotFound
- Un fichier YAML peut contenir plusieurs objets séparés par `---`
- Le namespace isole les **noms**, les **quotas** et les **droits**, pas le **réseau**
- Fiche associée : [Namespace](../../fiches/03-namespace.md)
