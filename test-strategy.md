# Stratégie de test — QuickOrder

## 1. Périmètre

Le périmètre de test couvre les parcours critiques de l'application de commande de repas :

- inscription et authentification ;
- consultation des restaurants et des produits ;
- gestion du panier et des quantités ;
- validation de commande et paiements ;
- gestion des adresses et profil utilisateur ;
- avis et notation des restaurants ;
- API REST et Swagger ;
- administration et suivi des commandes.

## 2. Hors périmètre

- tests de sécurité avancés (pentest, injection SQL, XSS, CSRF) ;
- tests multi-navigateur exhaustifs ;
- tests de disponibilité réseau ou de reprise après panne ;
- validation du design graphique purement esthétique ;
- tests utilisateur avec un grand panel de profils.

## 3. Parcours critiques

1. Création d'un compte / connexion.
2. Consultation d'un restaurant et d'un menu.
3. Ajout et modification d'un panier.
4. Vérification du stock et des quantités.
5. Finalisation d'une commande avec paiement simulé.
6. Validation des règles de coupon, de livraison et de montant minimum.
7. Consultation du profil et des adresses.
8. Publication d'un avis sur un restaurant.
9. Vérification de la cohérence des données côté API.

## 4. Risques métier et techniques

- rupture de stock non contrôlée ;
- commande acceptée avec paiement insuffisant ;
- ajout de produit épuisé dans le panier ;
- avis de restaurant publié sans historique commande ;
- validation insuffisante de l'adresse et des champs ;
- doublons de commande sur paiement PayPal ;
- comportements incohérents entre l'interface et l'API.

## 5. Types de tests

- tests fonctionnels ;
- tests de régression ciblée sur les parcours critiques ;
- tests limites et validations de saisie ;
- tests règles métier ;
- tests API de niveau 1 avec clé Swagger ;
- tests d'intégration UI / backend.

## 6. Priorisation risque × impact

| Priorité | Risque | Impact | Justification |
|---|---|---:|---|
| P1 | Stock / commande / paiement | Très élevé | Impact direct sur la satisfaction client et la cohérence transactionnelle |
| P1 | Paiement insuffisant / doublon | Très élevé | Risque financier et légal |
| P1 | Avis et historique d'achat | Élevé | Risque de confiance et de fraude |
| P2 | Validation d'adresse et nom | Moyen | Impact sur intégrité des données |
| P2 | Gestion des coupons | Moyen | Impact commercial et budget |
| P3 | Ergonomie / affichage | Faible à moyen | Impact sur expérience utilisateur mais pas sur la transaction |

## 7. Méthodologie

La campagne s'appuie sur :

- tests manuels sur l'interface web ;
- contrôles réseau et console navigateur ;
- validation API via Swagger / OpenAPI ;
- reproduction de scénarios sur données de démonstration ;
- documentation des écarts entre résultat attendu et obtenu.

## 8. Critère d'acceptation

Le produit ne peut pas être considéré comme prêt pour la mise en production si au moins une anomalie critique ou haute priorité reste non corrigée sur les parcours transactionnels de base.

Pour cette campagne, la recommandation est un No-Go, car plusieurs défauts critiques impactent directement les ventes, la fiabilité des stocks et la confiance utilisateur.
