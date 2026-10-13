# Plan d'amélioration — QuickOrder

## Priorité 1 — Sécuriser les transactions

1. Bloquer les commandes si le stock est insuffisant avant validation du panier.
2. Vérifier le montant cash reçu avant confirmation de commande.
3. Empêcher la création de commandes dupliquées pour PayPal.
4. Refuser les produits épuisés ou indisponibles dans le panier.

## Priorité 2 — Renforcer les règles métier

5. Vérifier que l'utilisateur a bien commandé dans le restaurant avant de publier un avis.
6. Contrôler la validité des adresses et les longueurs maximales des champs.
7. Appliquer le statut du restaurant (ouvert/fermé) à la validation de commande.

## Priorité 3 — Moderniser le parcours qualité

8. Ajouter des validations front-end et back-end sur tous les formulaires critiques.
9. Mettre en place une surveillance des stocks et des commandes en temps réel.
10. Automatiser les tests de régression sur les parcours critiques.

## Justification

Ces actions ciblent les risques critiques identifiés durant la campagne. Elles réduisent les erreurs de gestion, la fraude et les pertes commerciales tout en améliorant la confiance client et la qualité opérationnelle.
