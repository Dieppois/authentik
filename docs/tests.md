# Recette TP2

| Test | Attendu | Observé | Preuve |
|---|---|---|---|
| Identités et attributs | 3 comptes conformes | alice, bob, charlie internes, actifs, attributs corrects | [utilisateurs](../pictures/tp2-etape2-utilisateurs.png), vérification en base |
| Suspension puis retour de Bob | Refus, puis connexion | `login_failed` puis `login` après réactivation | [refus](../pictures/tp2-etape4-bob-refuse.png), journal Authentik |
| Groupes métier | RH, Dev, Admin attribués | alice RH, bob Dev, charlie Admin, aucun superutilisateur | [groupes](../pictures/tp2-etape6-groupes.png) |
| Compte sans facteur après MFA obligatoire | Refus | Non réalisé | - |
| Charlie avec TOTP valide | Succès | Connexion acceptée | Journal Authentik |
| Charlie avec TOTP incorrect | Refus | `login_failed` sur l'étape MFA | [refus TOTP](../pictures/tp2-etape10-charlie-totp-refuse.png) |
| Code de récupération utilisé deux fois | Succès, puis refus | `login` via Static Token, puis `login_failed` | [code réutilisé](../pictures/tp2-etape11-code-reutilise-refuse.png) |
| Alice dans Grafana | Viewer | Viewer, lecture seule | [rôles](../pictures/tp2-etape16-roles-grafana.png), [Alice](../pictures/tp2-etape16-dashboard-alice-viewer.png) |
| Bob dans Grafana | Editor avant départ | Editor, modification enregistrée (v4) | [Bob Editor](../pictures/tp2-etape16-dashboard-bob-editor.png) |
| Charlie dans Grafana | Admin d'organisation, pas admin global | Admin, `isGrafanaAdmin = false` | [rôles](../pictures/tp2-etape16-roles-grafana.png), API Grafana |
| Alice sans groupe autorisé | Refus à la nouvelle connexion | « Permission refusée » par Authentik | [Alice refusée](../pictures/tp2-etape16-alice-refusee.png) |
| Mobilité de Bob vers Audit | Viewer après nouvelle connexion | Viewer, plus de bouton Edit | [Bob Viewer](../pictures/tp2-etape16-dashboard-bob-viewer.png) |
| Dossiers RH et Dev | Accès conforme, y compris URL directe | Bob refusé sur RH, Alice refusée sur Dev (Forbidden) | [Bob](../pictures/tp2-etape17-bob-rh-refuse.png), [Alice](../pictures/tp2-etape17-alice-dev-refuse.png) |
| Bob désactivé dans l'IdP | Nouvelle authentification refusée | Refusée ; mais **4 sessions Grafana restent actives** | API Grafana `auth-tokens`, [refus étape 4](../pictures/tp2-etape4-bob-refuse.png) |
| Deprovisioning complet de Bob | Ancienne session et nouvel accès refusés | 0 session Grafana, aucun groupe, aucune équipe ; désactivation Grafana impossible (compte externe), profil retiré de l'organisation | API Grafana et `ak shell` |

**Test complémentaire** : `akadmin` via SSO Grafana → refusé (aucun groupe lié). Administrer l'IdP ne donne aucun droit applicatif.
