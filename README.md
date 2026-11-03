# ☸️ 100 Days of Kubernetes — KodeKloud

> Build in public de mon parcours Kubernetes sur les labs KodeKloud.
> Chaque lab = des manifests propres, une fiche de révision et, quand la notion s'y prête, un schéma d'architecture.

## 🎯 Objectif

Passer de « je sais lancer un pod » à « je comprends comment le cluster prend ses décisions » :
scheduling, réseau, stockage, sécurité, observabilité — avec une logique d'architecte Cloud/DevOps.

## 🗺️ Progression par jalons

| Jalon | Thème | Labs | Statut |
|-------|-------|------|--------|
| 1 | Fondamentaux : Pods, ReplicaSets, Deployments, Namespaces | 01-03 | 🔄 En cours |
| 2 | Services & réseau : ClusterIP, NodePort, Ingress, DNS | — | ⏳ À venir |
| 3 | Configuration : ConfigMaps, Secrets, variables d'env | — | ⏳ À venir |
| 4 | Scheduling : labels, selectors, taints/tolerations, affinity | — | ⏳ À venir |
| 5 | Stockage : Volumes, PV, PVC, StorageClass | — | ⏳ À venir |
| 6 | Sécurité : RBAC, ServiceAccounts, SecurityContext, NetworkPolicy | — | ⏳ À venir |
| 7 | Exploitation : probes, rolling updates, ressources, troubleshooting | — | ⏳ À venir |

> Les thèmes sont indicatifs et seront ajustés au fil des labs réels.

## 📂 Organisation du repo

```
labs/      → un dossier par lab : consigne résumée, manifests YAML, commandes utilisées
fiches/    → fiches de révision Markdown, une par notion
schemas/   → schémas d'architecture (Mermaid / PNG)
```

## 🧰 Stack

`kubectl` · `Kubernetes` · `YAML` · `Helm` (plus tard) · environnement de lab KodeKloud

## 📝 Méthode

1. Je lis la consigne du lab KodeKloud
2. Je le résous en comprenant chaque étape (pas de copier-coller aveugle)
3. Je documente la notion dans une fiche + un schéma si besoin
4. Je publie ici à chaque fin de jalon

---

⭐ Si ce parcours t'aide à apprendre Kubernetes, n'hésite pas à suivre le repo.
