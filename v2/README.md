# Projet de déploiement continu avec Azure Pipelines

Ce projet utilise Azure Pipelines pour mettre en œuvre un pipeline de déploiement continu pour une application web. Le pipeline comprend plusieurs étapes, y compris la validation du code, les tests, le déploiement canary, et la validation manuelle.

## Prérequis

Pour utiliser ce pipeline, vous aurez besoin de :

- Un compte Azure DevOps avec un projet configuré.
- Une application web à déployer.
- Un compte Docker Hub pour stocker vos images Docker.
- Un cluster Kubernetes pour déployer votre application.

## Configuration du pipeline

Le pipeline est défini dans le fichier `azure-pipelines.yml`. Vous pouvez le modifier pour l'adapter à vos besoins. Les variables utilisées dans le pipeline sont définies dans la section `variables` du fichier.

## Étapes du pipeline

1. **Validation de l'application** : Cette étape utilise SonarCloud pour analyser le code de l'application et détecter les problèmes de qualité du code.
2. **Test avec grype** : Cette étape utilise l'outil grype pour analyser les vulnérabilités de l'application.
3. **Vérification manuelle grype** : Si grype détecte des vulnérabilités, cette étape demande une vérification manuelle.
4. **Récupération de la version de l'application** : Cette étape récupère la version actuelle de l'application à partir du fichier `main.py`.
5. **Construction de l'image Docker** : Cette étape construit une nouvelle image Docker pour l'application et la pousse sur Docker Hub.
6. **Déploiement sur QAL** : Cette étape déploie l'application sur l'environnement QAL.
7. **Test de charge** : Cette étape effectue un test de charge sur l'application.
8. **Validation manuelle** : Si le test de charge échoue, cette étape demande une validation manuelle.
9. **Déploiement canary** : Cette étape déploie une version canary de l'application.
10. **Intervention manuelle** : Cette étape attend une validation manuelle avant de passer à l'étape suivante.
11. **Suppression du canary** : Si l'intervention manuelle échoue, cette étape supprime le déploiement canary.
12. **Déploiement sur Prod** : Si l'intervention manuelle réussit, cette étape déploie l'application sur l'environnement de production et supprime le déploiement canary.

## Utilisation

Pour utiliser ce pipeline, vous devez le configurer dans Azure DevOps et le connecter à votre dépôt GitHub. Vous pouvez ensuite déclencher le pipeline en apportant une modification à la branche master de votre dépôt.

