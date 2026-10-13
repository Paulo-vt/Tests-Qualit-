# Matrice des risques — QuickOrder

| ID | Domaine | Risque | Probabilité | Impact | Niveau | Mesure de contrôle |
|---|---|---|---|---:|---|---|
| R1 | Stock | Quantité négative et dépassement du stock | Élevée | Très élevé | Critique | Vérifier le stock avant validation et plafonner les quantités |
| R2 | Paiement | Validation d'un montant insuffisant | Élevée | Très élevé | Critique | Bloquer le paiement si le cash reçu est inférieur au total |
| R3 | Commande | Double commande PayPal | Moyenne | Très élevé | Critique | Empêcher la création de commandes dupliquées |
| R4 | Panier | Ajout d'un produit épuisé | Élevée | Élevé | Haute | Désactiver l'ajout ou bloquer le panier pour stock nul |
| R5 | Avis | Avis sans commande préalable | Élevée | Élevé | Haute | Vérifier le parcours d'achat avant publication |
| R6 | Profil | Données utilisateur non validées | Moyenne | Moyen | Moyenne | Limiter les longueurs et contrôler les formats |
| R7 | Adresse | Validation insuffisante des adresses | Moyenne | Moyen | Moyenne | Contrôler les champs obligatoires et le format |
| R8 | Coupon | Promotion non conforme à l'offre | Moyenne | Moyen | Moyenne | Vérifier la logique du coupon et l'affichage des montants |

## Synthèse

Les risques les plus critiques portent sur les transactions commerciales et le maintien de l'intégrité du stock. Les anomalies détectées touchent directement la confiance utilisateur et peuvent provoquer des pertes commerciales ou des erreurs de gestion.
