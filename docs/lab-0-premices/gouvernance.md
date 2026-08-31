# Gouvernance

## Découpage organisationnel Azure

Deux niveaux de découpage :

1. **Niveau métier** — Bancaire vs Événementiel
2. **Niveau environnement** (dans chaque métier) — Dev / Test / Prod

> Azure permet jusqu'à 6 niveaux de hiérarchie via les Management Groups. Le découpage à 2 niveaux retenu ici reste volontairement simple pour la taille du projet.

*À formaliser au Chapitre 3 (Landing Zone) : traduction concrète en abonnements Azure et management groups.*

## Rôles et accès

| Rôle | Périmètre |
|---|---|
| Équipe cloud | Gère l'infrastructure |
| Équipe sécurité | Monitore l'infrastructure |
| Développeurs | Dev et test uniquement, droit de créer des ressources sur ces environnements |
| Admin | Accès élevé — modalité en cours d'arbitrage (voir ci-dessous) |

### Point ouvert — Accès admin

Un accès admin permanent pose question au regard du principe de moindre privilège. Arbitrage à trancher au Chapitre 4 (Identité & accès) : accès élevé permanent, ou accès élevé temporaire/à la demande (type PIM/JIT) ?

## Nommage et tagging

**Tags obligatoires :**
- Environnement (dev / test / prod)
- Nom de l'application
- Propriétaire / équipe responsable (notification en cas de changement)

**Principe** : une règle de tagging ne vaut que si elle est appliquée et vérifiée, pas seulement documentée. Traduction technique prévue en policy-as-code, contrôlée en CI/CD.

**Lien FinOps** : ces tags serviront de base à l'allocation de coûts au Chapitre 11.
