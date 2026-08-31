# Définir le projet

## Fil conducteur

Construire une infra cloud digne d'une entreprise, chapitre par chapitre, documentée comme en entreprise réelle (README type ADR par chapitre).

## Objectifs

- Portfolio GitHub crédible pour un positionnement cloud sécurité / consultant Azure
- Contenu réutilisable pour un suivi de série sur LinkedIn à chaque chapitre terminé
- Montée en compétence pratique, en parallèle d'une préparation de certifications Azure
- Chaque chapitre = code + README ADR (contexte, décision, alternatives considérées, conséquences)

## Le business : Vybe

Néobanque B2C fictive, opérant en Europe (hors France).

**Concept** : un compte bancaire classique couplé à un accès privilégié à des événements (concerts, festivals). Exemple : assister à un concert déclenche un upgrade automatique ou l'obtention d'un goodie.

**Échelle** : scale-up européenne multi-pays.

## Cadre réglementaire

- **PSD2** — authentification forte du client (SCA), API ouvertes
- **Licence e-money (EMD2)** avec passporting UE
- **AML/KYC** — directives anti-blanchiment
- **RGPD** — vigilance particulière sur les données événementielles (voir [cartographie des données](./cartographie-donnees.md))
- **DORA** — résilience opérationnelle numérique
- **PCI-DSS** — si émission de cartes de paiement

## Structure du projet

0. Les prémices (gouvernance + cartographie des données)
1. Bootstrap : socle minimal Terraform
2. CI/CD : pipeline GitHub Actions
3. Landing Zone : réseau & gouvernance
4. Identité & accès sans secrets
5. Compute : orchestration de conteneurs
6. Déploiement applicatif GitOps
7. Secrets & configuration
8. Ingress, exposition & réseau applicatif
9. Données : base managée en haute disponibilité
10. Observabilité : métriques, logs, traces
11. FinOps : visibilité et gouvernance des coûts
12. Posture de sécurité continue
