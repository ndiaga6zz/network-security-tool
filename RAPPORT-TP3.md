\# TP3 — Audit de sécurité Docker avec Trivy



\## 1. Périmètre et adaptation

Projet repris du TP2.

Script interactif network\_check.py, sans API ni NGINX.

Parties de l'énoncé non applicables et raison.



\## 2. Infrastructure initiale

Service, image, ports, volumes et configuration.



\## 3. Scan avant durcissement

Date, version de Trivy, image analysée et résultats.



\## 4. Mesures appliquées

Utilisateur non-root.

Système de fichiers en lecture seule.

Suppression des capacités Linux.

Blocage de l'acquisition de nouveaux privilèges.



\## 5. Tests et scan après durcissement

Tests fonctionnels et comparaison avant/après.



\## 6. GitHub Actions

Construction, scan, résultat et interprétation des logs.



\## 7. Réponses aux questions

Q1 — Code source et image

Bandit examine le code Python ; Trivy examine ici les composants embarqués dans l’image, notamment ceux provenant de l’image de base. Les deux contrôles sont complémentaires.



Q2 — Port exposé et port publié

EXPOSE ou expose ne crée pas une publication sur l’hôte. Une publication avec ports permet l’accès via une adresse et un port de l’hôte. Ton programme ne nécessite ici aucun port publié.



Q3 — Isolation de la base

Un réseau backend limite les services pouvant joindre directement la base. Cette question reste théorique dans ton projet puisqu’il ne possède pas de base de données.



Q4 — Exécution root

Un processus compromis exécuté en root dispose de privilèges plus importants dans le conteneur. L’utilisateur non-root réduit ces privilèges, sans garantir à lui seul une isolation parfaite.



Q5 — Gravité et identifiants

HIGH et CRITICAL sont des niveaux de gravité. Une CVE identifie publiquement une vulnérabilité. La version corrigée indique une version du composant dans laquelle une correction est disponible.



Q6 — --exit-code 1

Ce paramètre permet de retourner un code d’échec si le scan détecte des vulnérabilités correspondant aux filtres. En CI, il transforme le scan en contrôle bloquant pour les étapes qui en dépendent.



Q7 — Absence de CVE

Le résultat dépend des composants identifiés, de la base de vulnérabilités et des filtres. Il ne démontre pas que le code ou la configuration ne comporte aucun problème.



Q8 — Risques restants

Des erreurs de code, des secrets exposés, des privilèges excessifs ou des failles encore inconnues peuvent subsister malgré les mises à jour. D’où l’intérêt de combiner analyses, durcissement et tests.

