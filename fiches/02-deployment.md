# Fiche — Le Deployment

## 📌 En une phrase

Le **Deployment** décrit l'état voulu d'une application (image, nombre de réplicas) et Kubernetes s'occupe en permanence de le faire respecter : auto-réparation, scaling et mises à jour sans coupure.

> Analogie : le Pod est un employé, le ReplicaSet est le chef d'équipe qui remplace tout absent, le Deployment est le RH qui gère les changements de poste (nouvelle version) sans fermer le service.

## 🏗️ La hiérarchie

```mermaid
flowchart TD
    D["Deployment httpd<br/>(stratégie, historique de versions)"]
    RS1["ReplicaSet httpd-5d8f…<br/>(garantit N réplicas)"]
    P1["Pod httpd-5d8f…-abcde"]
    P2["Pod httpd-5d8f…-fghij"]
    D -->|crée et pilote| RS1
    RS1 -->|crée / remplace| P1
    RS1 -->|crée / remplace| P2
    L(["label app=httpd"]) -.relie.- D
    L -.relie.- RS1
    L -.relie.- P1
    L -.relie.- P2
```

## 🔄 Rolling update (changement d'image)

```mermaid
flowchart LR
    subgraph Avant
        A1[RS v1 : 3 pods]
    end
    subgraph Pendant
        B1[RS v1 : 2 pods] --- B2[RS v2 : 1 pod]
    end
    subgraph Après
        C1[RS v1 : 0 pod<br/>conservé pour rollback] --- C2[RS v2 : 3 pods]
    end
    Avant --> Pendant --> Après
```

L'ancien ReplicaSet est gardé à 0 réplica : c'est ce qui rend `kubectl rollout undo` instantané.

## 📄 Anatomie du manifest

```yaml
apiVersion: apps/v1        # ⚠️ apps/v1, pas v1
kind: Deployment
metadata:
  name: httpd
spec:
  replicas: 1
  selector:
    matchLabels:
      app: httpd           # ① quels pods je gère…
  template:                # ② …le modèle de ces pods
    metadata:
      labels:
        app: httpd         # doit correspondre à ①
    spec:
      containers:
        - name: httpd
          image: httpd:latest
```

## ⌨️ Commandes clés

| Besoin | Commande |
|---|---|
| Créer | `kubectl create deployment <nom> --image=<img>` |
| Générer le YAML | `... --dry-run=client -o yaml` |
| Scaler | `kubectl scale deployment <nom> --replicas=3` |
| Changer l'image | `kubectl set image deployment/<nom> <container>=<img:tag>` |
| Suivre un déploiement | `kubectl rollout status deployment/<nom>` |
| Historique | `kubectl rollout history deployment/<nom>` |
| Revenir en arrière | `kubectl rollout undo deployment/<nom>` |
| Voir toute la chaîne | `kubectl get deploy,rs,pods -l app=<nom>` |

## 🚨 Pièges courants

- `apiVersion: apps/v1` (et non `v1` comme pour un Pod)
- `selector` qui ne correspond pas aux labels du template → erreur à la création
- Le container s'appelle comme l'image (`httpd`) avec `kubectl create deployment`
- `:latest` en prod = version non maîtrisée → épingler un tag précis

## 🎤 Question d'entretien

**Quelle différence entre un ReplicaSet et un Deployment ?**
Le ReplicaSet maintient un nombre de pods identiques. Le Deployment gère des ReplicaSets successifs pour faire des mises à jour progressives et des rollbacks. On ne manipule quasiment jamais un ReplicaSet directement.
