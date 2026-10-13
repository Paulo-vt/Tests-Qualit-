# Rapport d'exécution de campagne — QuickOrder

## 1. Période

Campagne QA de validation de la version de démonstration QuickOrder, avant mise en production.

## 2. Méthode

- validation fonctionnelle sur le parcours utilisateur ;
- vérification des règles métier ;
- contrôle API via Swagger/OpenAPI ;
- reproduction de scénarios d'erreur et de limite ;
- collecte des anomalies dans des bug reports structurés.

## 3. Résultats

| Catégorie | Nombre | Pourcentage |
|---|---:|---:|
| Cas de test totaux | 24 | 100% |
| Pass | 16 | 66,7% |
| Fail | 8 | 33,3% |
| Blocked | 0 | 0% |
| Skipped | 0 | 0% |

## 4. Points de vigilance majeurs

- rupture du stock non sécurisée ;
- montant cash insuffisant accepté ;
- doublons de commande PayPal ;
- catalogue non protégé contre les produits épuisés ;
- avis laissés sans historique de commande ;
- validation des adresses et noms insuffisante.

## 5. Recommandation

La recommandation est un No-Go pour la mise en production dans l'état actuel.

Les anomalies détectées concernent les fonctions transactionnelles les plus sensibles du produit. Elles ont un impact direct sur la satisfaction client, la sécurité des données et la fiabilité opérationnelle.

## 6. Conclusion

Le produit a été testé sur les parcours critiques et les règles métier essentielles. Les résultats montrent qu'il reste fonctionnel sur les usages principaux, mais des défauts sérieux subsistent sur la gestion des stocks, des paiements et des contrôles d'intégrité métier.
