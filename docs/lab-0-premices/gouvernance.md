# Gouvernance
 
## Découpage organisationnel Azure
 
### Hiérarchie retenue : 3 niveaux
 
```
Vybe (racine)
├── Platform (ressources partagées)
├── Bancaire
│   ├── Dev
│   ├── Test
│   └── Prod
└── Événementiel
    ├── Dev
    ├── Test
    └── Prod
```
 
### Pourquoi un niveau racine "Platform"
 
Le premier découpage envisagé s'arrêtait à 2 niveaux (métier, puis environnement). En creusant, deux limites sont apparues :
 
- **Des ressources doivent être partagées** entre le bancaire et l'événementiel (monitoring central, identité commune, policies de sécurité globales) — un découpage à 2 niveaux ne leur donne pas de place naturelle, elles finiraient dupliquées ou mal rattachées à un seul métier.
- **Le découpage doit pouvoir accueillir un futur métier** (ex : une offre d'assurance liée aux événements) sans tout redécouper. Un niveau racine qui chapote les domaines métier rend cette extension naturelle : on ajoute un nouveau domaine au même niveau que Bancaire/Événementiel, sans toucher à l'existant.
Cette structure s'aligne sur le **Cloud Adoption Framework (CAF) de Microsoft**, et plus précisément son modèle *Enterprise-Scale Landing Zone*, qui distingue justement un niveau "Platform" (ressources et services partagés à toute l'organisation) des "Landing Zones" propres à chaque domaine métier. Le CAF sert ici de référence pour valider que la structure retenue correspond à un pattern reconnu, pas à une improvisation.
 
### Pourquoi séparer Bancaire et Événementiel
 
- **Conformité différenciée** : le périmètre bancaire et le périmètre événementiel ne répondent pas aux mêmes normes (PSD2/DORA côté bancaire, exigences différentes côté billetterie/partenariats). Les séparer permet d'appliquer des politiques de sécurité et de conformité adaptées à chaque domaine, sans sur-contraindre l'un ou sous-contraindre l'autre.
- **Confinement du rayon d'explosion (blast radius)** : le périmètre événementiel est plus exposé (billetterie ouverte, partenaires externes) et donc plus à risque. En cas de compromission côté événementiel, la séparation garantit que le périmètre bancaire — le plus critique — n'est pas affecté.
## Rôles et accès — moindre privilège
 
| Rôle | Périmètre |
|---|---|
| Équipe cloud | Gère l'infrastructure |
| Équipe sécurité | Monitore l'infrastructure |
| Développeurs | Dev et test uniquement, droit de créer des ressources sur ces environnements |
| Admin (moi) | Accès élevé — **temporaire/à la demande, pas permanent** |
 
**Principe appliqué : le moindre privilège s'applique à tout le monde, y compris à l'administrateur du projet.** Un accès admin permanent, même pour soi-même, va à l'encontre du principe qu'on cherche justement à appliquer à toute l'organisation — un accès élevé doit être activé à la demande, tracé, et limité dans le temps plutôt que disponible en permanence. Modalité technique précise (type PIM/JIT) à détailler au Lab 4 (Identité & accès).
 
## Nommage et tagging
 
**Tags obligatoires :**
- **Environnement** (dev / test / prod) — usage organisationnel : sait immédiatement dans quel contexte se trouve une ressource, évite les erreurs de manipulation entre environnements
- **Nom de l'application** — usage organisationnel et FinOps : permet de retrouver rapidement à quel service une ressource appartient, et de regrouper les coûts par application
- **Propriétaire / équipe responsable** — usage organisationnel et FinOps : permet d'être notifié en cas de changement sur la ressource, et d'allouer les coûts à la bonne équipe pour la responsabilisation budgétaire
**Double finalité assumée** : ces tags ne servent pas qu'à s'y retrouver au quotidien (organisationnel), ils posent aussi la base de l'allocation de coûts qui sera exploitée au Lab 11 (FinOps) — sans tagging cohérent dès le départ, aucune analyse de coûts fiable n'est possible a posteriori.
 
**Principe** : une règle de tagging ne vaut que si elle est appliquée et vérifiée, pas seulement documentée. Traduction technique prévue en policy-as-code, contrôlée en CI/CD.
