# Matrice RBAC Nova Services

Les groupes Authentik représentent les catégories métier. Grafana les traduit en rôles applicatifs.

## Groupes et rôles Grafana

| Groupe Authentik | Membre initial | Rôle Grafana | Portée |
|---|---|---|---|
| Admin | Charlie | Admin | Administration de l'organisation Grafana |
| Dev | Bob | Editor | Création et modification des tableaux de bord autorisés |
| RH | Alice | Viewer | Consultation des tableaux de bord autorisés |
| Audit | Aucun | Viewer | Consultation des tableaux de bord autorisés |

## Limites de la matrice

- **Admin** = administrateur de l'organisation Grafana, pas **GrafanaAdmin** (administration globale du serveur).
- **Editor** n'est pas limité au dossier Dev : il peut modifier tout tableau de bord autorisé.
- **Audit** ne donne accès ni aux journaux Authentik ni à une fonction d'audit payante.
- Aucun groupe n'est superutilisateur Authentik.
- Les rôles de base ne séparent pas les tableaux de bord par département : il faut des permissions de dossiers.

## Équipes Grafana

| Équipe | Membres | Gestion |
|---|---|---|
| nova-dev | bob (charlie, créateur) | Manuelle |
| nova-rh | alice (charlie, créateur) | Manuelle |

Le mapping OIDC ne synchronise pas les équipes : à mettre à jour lors d'une mobilité ou d'un départ.

## Permissions des dossiers

Rôles généraux Viewer et Editor retirés des deux dossiers.

| Dossier | Admin (rôle) | charlie | nova-dev | nova-rh |
|---|---|---|---|---|
| Dev | Admin | Admin | **Edit** | - |
| RH | Admin | Admin | - | **View** |

## Accès effectifs

| Compte | Rôle org | Dossier Dev | Dossier RH | Dossier General |
|---|---|---|---|---|
| bob | Editor | Consultation et modification | Refusé (URL directe testée) | Modification |
| alice | Viewer | Refusé (URL directe testée) | Lecture seule | Lecture seule |
| charlie | Admin | Administration | Administration | Administration |

Limite : les permissions de dossiers ne protègent pas les sources de données interrogées.
