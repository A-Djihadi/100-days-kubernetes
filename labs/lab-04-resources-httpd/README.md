# Lab 04 — Requests et limits sur un pod httpd

## 🎯 Consigne

- Pod `httpd-pod`, container `httpd-container`, image `httpd:latest`
- Requests : mémoire `15Mi`, CPU `100m`
- Limits : mémoire `20Mi`, CPU `100m`

## 🛠️ Résolution

```bash
kubectl apply -f httpd-pod.yaml

# Vérifier
kubectl get pod httpd-pod
kubectl get pod httpd-pod -o jsonpath='{.spec.containers[0].resources}{"\n"}'
kubectl get pod httpd-pod -o jsonpath='{.status.qosClass}{"\n"}'   # → Burstable
```

## 💡 Ce que j'ai retenu

- YAML obligatoire : `kubectl run` ne gère plus `--requests` / `--limits`
- Request = réservation (scheduler) ; limit = plafond (kubelet / cgroups)
- CPU dépassé → throttling ; mémoire dépassée → OOMKilled
- requests ≠ limits sur la mémoire → QoS **Burstable**
- Fiche associée : [Requests & Limits](../../fiches/04-resources-requests-limits.md)
