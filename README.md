****Manifests Kubernetes de l'application****

Manifests Kubernetes de l'application FastAPI full-stack (backend, frontend, PostgreSQL, Adminer).

**Source de référence :**

Le déploiement automatisé utilise le chart Helm du dépôt infras (fastapi/app).

**Contenu**

**Fichier	Objet**

back-deployement.yml, back-service.yml	Backend FastAPI, 2 réplicas, probes sur /api/v1/utils/health-check/
front-deployement.yml, front-service.yml	Frontend, 2 réplicas
db-deployement.yaml, services-db.yml	PostgreSQL 12 en StatefulSet
pv.yaml, pvc-db.yaml	Stockage 5 Gi de la base (hostPath, mono-nœud)
prestart-job.yml	Job de migration et d'initialisation (scripts/prestart.sh)
adminer-*	Interface d'administration de la base (usage interne uniquement)
ingress.yaml	Routage Traefik : /api vers le backend, / vers le frontend
Avant d'appliquer


**Prérequis cluster**

Un contrôleur Traefik (ingressClassName: traefik), un load balancer (MetalLB) et, pour le TLS, cert-manager. Voir infras.

**Limites connues**

Base en instance unique, volume hostPath : les données restent sur un seul nœud.
Adminer ne doit pas être exposé publiquement.
