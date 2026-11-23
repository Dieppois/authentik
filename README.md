# TP1 Nova Services : Authentik, Grafana et Gitea avec Docker

Plateforme IAM de Nova Services (Authentik) et deux applications (Grafana, Gitea) lancées avec Docker Compose.

## Prérequis

- Docker Desktop démarré (Compose v2 avec `up --wait`)
- Python 3.9 ou plus (sous Windows : `python`)
- Git
- Ports libres sur l'hôte : 3000, 3001, 9000, 9443

## Lancement

```bash
python scripts/init_env.py          # une seule fois, crée .env
docker compose pull
docker compose up -d --wait --wait-timeout 600
docker compose ps
```

| Service | URL |
|---|---|
| Authentik | http://localhost:9000 |
| Grafana | http://localhost:3000 |
| Gitea | http://localhost:3001 |

## Pause et reprise

```bash
docker compose stop                              # pause
docker compose up -d --wait --wait-timeout 600   # reprise
docker compose down                              # supprime conteneurs et réseau, garde les volumes
```

Ne jamais utiliser `down -v` : les volumes contiennent les bases Authentik, Grafana et Gitea.

## Documentation

- TP1 (installation) : [Doc.md](Doc.md)
- TP2 (identités, RBAC, MFA, SSO OIDC) : [Doc-TP2.md](Doc-TP2.md)
