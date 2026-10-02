# Passerelle

Suivi d'alternance et de stage pour les écoles privées post-bac.
Documentation : `docs/` · Charte d'architecture : `AGENTS.md`

## Prérequis
Java 21, Node 22, Docker.

## Lancer en local
```bash
docker compose up -d db                 # PostgreSQL sur le port 5432
cd backend && ./mvnw spring-boot:run    # API sur http://localhost:8080
cd frontend && npm install && npm run dev   # interface sur http://localhost:3000
```

## Vérifier avant de proposer un commit
```bash
cd backend && ./mvnw verify             # tests, règles d'architecture, couverture
cd frontend && npm run check            # lint, types, règles de dépendance, tests
```

## Structure
Un monolithe modulaire : un package par contexte métier (voir `docs/02-domaine.md`).
Les règles de dépendance sont vérifiées par `ArchitectureTest` : lire `AGENTS.md` avant de contribuer.
