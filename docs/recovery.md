# Procédures de récupération

Aucun secret dans ce document.

## Perte du second facteur

**Prérequis** : chaque compte sensible (akadmin, charlie) possède des codes Static de secours, conservés hors du téléphone.

1. Vérifier l'identité du demandeur selon la procédure de support
2. Révoquer le périphérique perdu, examiner sessions et événements suspects
3. Révoquer les sessions compromises ou douteuses, y compris dans les applications
4. Se connecter avec un code de secours ou une récupération contrôlée
5. Enrôler le nouveau périphérique, vérifier une nouvelle connexion
6. Renouveler les codes de secours si leur confidentialité est incertaine

> ⚠️ Avec l'action **Deny**, supprimer tous les périphériques d'un utilisateur ne lui rend pas l'accès : il est refusé. Sans facteur de secours, l'administrateur organise une récupération contrôlée (enrôlement encadré).

**Testé** : connexion de Charlie avec un code de secours, puis refus du même code (usage unique).

## Secours Grafana (panne de l'IdP)

**Prérequis** : mot de passe du compte local `admin` Grafana conservé dans un coffre.

1. Un administrateur de l'hôte modifie le service `grafana` dans `docker-compose.yml` :
   - `GF_AUTH_DISABLE_LOGIN_FORM: "false"`
   - `GF_AUTH_BASIC_ENABLED: "true"`
2. Recréer Grafana : `docker compose up -d --no-deps --force-recreate grafana`
3. Se connecter avec `admin` via le formulaire local et intervenir
4. Rétablir `"true"` et `"false"`, puis recréer Grafana
5. Tracer l'intervention (date, auteur, motif)

> ⚠️ Procédure réservée aux administrateurs de l'infrastructure. Elle ne doit pas devenir un chemin quotidien contournant le MFA.
