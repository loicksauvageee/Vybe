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

## Flux événementiel

- Billetterie fermée, uniquement via des partenaires officiels Vybe
- Achat du billet directement dans l'app Vybe
- Les billetteries partenaires affichent le partenariat Vybe (co-branding)

## Principe architectural — Minimisation par design

Vybe n'a pas besoin de savoir *qui précisément* était à un événement — uniquement des données agrégées (ex : nombre d'utilisateurs Vybe présents à un concert donné). Pas de traçage individuel nominatif de la présence.

Ce principe influence directement le Chapitre 3 (Landing Zone) et le Chapitre 9 (Données) : la donnée de présence individuelle n'est pas stockée durablement sous forme identifiable — seule l'agrégation est conservée.

## Analyse RGPD — Article 9

L'article 9 du RGPD liste 8 catégories de données sensibles : origine raciale/ethnique, opinions politiques, convictions religieuses/philosophiques, appartenance syndicale, données génétiques, biométriques, de santé, vie sexuelle/orientation sexuelle. Le traitement de ces données est interdit par principe, sauf exceptions.

La CJUE a une lecture extensive : une donnée en apparence anodine peut être requalifiée en donnée sensible si elle permet une inférence vers une des 8 catégories.

**Conclusion retenue** : dans le cas général (concert, match, musée), le type d'événement ne constitue pas une donnée sensible au sens Art. 9.

**Point de vigilance** : certains cas limites pourraient basculer dans la logique d'inférence de la CJUE (événement religieux, marche des fiertés, rassemblement politique) — à traduire en règle métier (catégorisation d'événements à traitement renforcé, ou exclusion du programme).

**Au-delà du légal** : même hors qualification RGPD stricte, la sensibilité perçue par l'utilisateur justifie l'anonymisation/agrégation par défaut — enjeu de confiance autant que de conformité.
