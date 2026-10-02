# Décisions d'architecture

*Cinq ADR, un fichier par décision*

Cinq décisions structurantes, numérotées. Une décision ne se réécrit pas : on la remplace par une nouvelle fiche qui explique pourquoi (règle 4 de l'énoncé). Les ADR 001, 002 et 003 sont ceux que l'énoncé exige ; les ADR 004 et 005 consignent deux décisions de produit qui pèsent sur l'architecture.

| ADR | Décision |
|---|---|
| [ADR-001](0001-style.md) | Style d'architecture : monolithe modulaire, hexagonal dans chaque module |
| [ADR-002](0002-stack.md) | Stack : Java 21 / Spring Boot, Next.js, PostgreSQL, PaaS européen |
| [ADR-003](0003-patterns.md) | Patterns retenus et patterns interdits |
| [ADR-004](0004-confidentialite.md) | Confidentialité par conception : l'école ne voit que le statut global |
| [ADR-005](0005-pas-de-scraping.md) | Offres issues de sources officielles uniquement, aucun scraping |
