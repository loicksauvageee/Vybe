# Cartographie des données

## Catégories de données identifiées

- **Identité personnelle** — nom, prénom, âge, adresse
- **Documents officiels / KYC** — passeport, carte d'identité, justificatif de domicile
- **Préférences événementielles** — types d'événements préférés (concerts, sport, musées...)
- **Données bancaires / transactionnelles** — comptes, transactions, moyens de paiement

## Classement par sensibilité

| Catégorie | Niveau | Notes |
|---|---|---|
| Données bancaires/transactionnelles | Critique | Impact direct si fuite |
| Localisation à un instant T (event + date) | Critique | Aussi sensible que la donnée bancaire |
| Documents officiels / KYC | Critique | Risque d'usurpation d'identité |
| Identité personnelle | Élevé | Base RGPD classique |
| Préférences événementielles déclarées | Modéré | Non sensible au sens Art. 9 dans le cas général — voir analyse RGPD |

## Durée de conservation

| Catégorie | Durée retenue | Justification |
|---|---|---|
| Documents officiels / KYC | 5 ans après fin de relation client | Obligation légale type AML — conservation minimale après clôture du compte |
| Données bancaires/transactionnelles | 5 ans après fin de relation client | Même logique, obligation légale AML/DORA |
| Identité personnelle | Durée de la relation client + 5 ans | Alignée sur KYC, base commune |
| Préférences événementielles | 24 mois d'inactivité, puis anonymisation | Pas d'obligation légale — choix produit, pas de raison de garder une donnée comportementale au-delà d'un usage raisonnable |

*Point à valider avec un DPO dans un contexte réel — durées données à titre indicatif pour ce projet fictif.*

## Localisation des données (résidence)

**Contrainte** : les données doivent rester hébergées en UE, cohérent avec la licence e-money et le passporting européen — aucune donnée ne doit sortir de l'UE, y compris pour du traitement secondaire (analytics, backups).

**Région Azure retenue pour ce projet : Sweden Central.** Choix pratique lié à la disponibilité de cette région sur l'abonnement étudiant utilisé pour le projet — dans un contexte de production réel, le choix de région se ferait plutôt sur la localisation de la majorité des utilisateurs et la latence. Ce choix est documenté et justifié plus en détail au [Lab 3 — Landing Zone](../labs/lab-3-landing-zone-reseau).

Toutes les catégories de données (bancaire et événementiel) sont hébergées dans la même région pour ce projet — pas de séparation géographique entre les deux métiers.

## Propriétaires des données

| Catégorie | Équipe propriétaire | Notes |
|---|---|---|
| Données bancaires/transactionnelles | Bancaire | Cohérent avec le découpage organisationnel |
| Préférences événementielles | Événementiel | Cohérent avec le découpage organisationnel |
| Documents officiels / KYC | Bancaire | Rattaché au métier le plus contraint réglementairement |
| Identité personnelle | Platform | Donnée transverse aux deux métiers — rattachée au niveau partagé plutôt qu'à l'un ou l'autre, pour éviter une duplication ou un flou de responsabilité |

## Flux événementiel

- Billetterie fermée, uniquement via des partenaires officiels Vybe
- Achat du billet directement dans l'app Vybe
- Les billetteries partenaires affichent le partenariat Vybe (co-branding)

## Principe architectural — Minimisation par design

Vybe n'a pas besoin de savoir *qui précisément* était à un événement — uniquement des données agrégées (ex : nombre d'utilisateurs Vybe présents à un concert donné). Pas de traçage individuel nominatif de la présence.

Ce principe influence directement le Lab 3 (Landing Zone) et le Lab 9 (Données) : la donnée de présence individuelle n'est pas stockée durablement sous forme identifiable — seule l'agrégation est conservée.

## Analyse RGPD — Article 9

L'article 9 du RGPD liste 8 catégories de données sensibles : origine raciale/ethnique, opinions politiques, convictions religieuses/philosophiques, appartenance syndicale, données génétiques, biométriques, de santé, vie sexuelle/orientation sexuelle. Le traitement de ces données est interdit par principe, sauf exceptions.

La CJUE a une lecture extensive : une donnée en apparence anodine peut être requalifiée en donnée sensible si elle permet une inférence vers une des 8 catégories.

**Conclusion retenue** : dans le cas général (concert, match, musée), le type d'événement ne constitue pas une donnée sensible au sens Art. 9.

**Point de vigilance** : certains cas limites pourraient basculer dans la logique d'inférence de la CJUE (événement religieux, marche des fiertés, rassemblement politique) — à traduire en règle métier (catégorisation d'événements à traitement renforcé, ou exclusion du programme).

**Au-delà du légal** : même hors qualification RGPD stricte, la sensibilité perçue par l'utilisateur justifie l'anonymisation/agrégation par défaut — enjeu de confiance autant que de conformité.

---

*Points volontairement traités de façon succincte, hors du périmètre technique de ce projet : base légale du traitement par catégorie, gestion des sous-traitants (DPA avec les billetteries partenaires), chiffrement détaillé par catégorie, modalités d'exercice des droits des personnes. Ces sujets relèveraient d'un DPO dans un contexte réel.*
