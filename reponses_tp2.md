\# Réponses — TP2 GitHub Actions



\## Question 1 — Pourquoi les tests ne dépendent-ils pas de l'ouverture réelle du port 443 ?



Le test utilisant le port 443 appelle uniquement is\_valid\_port.

Cette fonction vérifie que la valeur est un entier compris

entre 1 et 65535. Elle ne tente aucune connexion réseau.



Le test appelant check\_port utilise le port invalide 70000.

La fonction déclenche une ValueError avant de créer la socket.



Aucun de ces tests ne dépend donc d'un service réseau actif.



\## Question 2 — Quelle différence entre push et pull\_request ?



L'événement push correspond à l'envoi de commits vers une branche

du dépôt distant.



L'événement pull\_request concerne une demande d'intégration

de modifications entre deux branches, notamment lors de son

ouverture ou de sa mise à jour.



Dans ce workflow, les push sont suivis sur main et feature/\*\*.

Les Pull Requests sont suivies lorsqu'elles ciblent main.



\## Question 3 — Que se passe-t-il si pytest renvoie un code d'erreur ?



L'étape Run unit tests est marquée en échec et le job échoue.



Avec ce workflow, l'étape Bandit suivante est normalement ignorée,

car elle dépend du succès des étapes précédentes.



L'échec est visible dans GitHub Actions et dans les vérifications

de la Pull Request.



\## Question 4 — Pourquoi est-il utile de bloquer l'intégration d'une Pull Request lorsque les tests échouent ?



Cela évite d'intégrer dans la branche principale des modifications

qui ne respectent pas le comportement attendu.



Les erreurs peuvent être corrigées avant la fusion, ce qui limite

les régressions et améliore la fiabilité du projet.



Pour imposer ce blocage sur GitHub, il faut configurer une règle

de protection de branche ou un ruleset exigeant la réussite

des vérifications. Le workflow seul ne garantit pas ce blocage.



\## Question 5 — Quelle différence entre ce contrôle SAST et les tests fonctionnels pytest ?



Bandit effectue une analyse statique de sécurité du code Python.

Il recherche des constructions potentiellement dangereuses

sans exécuter le programme pour tester son comportement.



Pytest exécute les fonctions à travers les tests et compare

les résultats obtenus aux résultats attendus.



Ces contrôles sont complémentaires : les tests vérifient les

comportements couverts, tandis que Bandit recherche certains

problèmes de sécurité dans le code.



\## Observation du pipeline volontairement échoué



Test en échec : test\_valid\_port



Ligne d'erreur observée : Error: Process completed with exit code 1.

