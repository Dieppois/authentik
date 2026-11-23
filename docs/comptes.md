# Comptes Nova Services

## Identités

| Username | Nom | Email | Type | Path |
|---|---|---|---|---|
| `alice` | Alice Martin | alice@nova-services.test | Interne | users |
| `bob` | Bob Dupont | bob@nova-services.test | Interne | users |
| `charlie` | Charlie Bernard | charlie@nova-services.test | Interne | users |

Adresses `.test` fictives. Mots de passe uniques, conservés hors du dépôt.

## Attributs métier

| Utilisateur | Département | Attribut `role` | Niveau |
|---|---|---|---|
| alice | RH | Manager RH | 2 |
| bob | Development | Backend Developer | 1 |
| charlie | IT | System Administrator | 5 |

- `clearance_level` stocké en nombre
- Attributs gérés par l'administrateur uniquement
- Aucun droit n'est donné par ces attributs

## État initial

| Compte | Actif | Groupe | Accès Grafana |
|---|---|---|---|
| alice | Oui | Aucun | Aucun |
| bob | Oui | Aucun | Aucun |
| charlie | Oui | Aucun | Aucun |

## Appartenances (étape 6)

| Compte | Groupe |
|---|---|
| alice | RH |
| bob | Dev |
| charlie | Admin |

## État final

| Compte | Actif | Groupe | Accès Grafana |
|---|---|---|---|
| alice | Oui | RH | Viewer, dossier RH en lecture |
| bob | **Non** | Aucun | Aucun : sessions révoquées, retiré de l'équipe et de l'organisation |
| charlie | Oui | Admin | Admin d'organisation |
| mfa-test | Non créé | - | - |

Bob n'est pas supprimé d'Authentik : compte désactivé, conservé selon la politique de conservation.
