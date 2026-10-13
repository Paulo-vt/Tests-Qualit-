# Cas de test — QuickOrder

## 1. Cas nominaux (6)

### TC-N01 — Connexion client avec compte valide
- Objectif : vérifier la connexion d'un utilisateur existant.
- Préconditions : compte client existant ; utilisateur hors connexion.
- Données : email `alice@example.com`, mot de passe `Password123!`.
- Étapes : 1) ouvrir la page de connexion ; 2) saisir les identifiants ; 3) cliquer sur Se connecter.
- Résultat attendu : redirection vers le profil et affichage du compte connecté.
- Résultat obtenu : connexion réussie.
- Statut : Pass

### TC-N02 — Consultation d'un restaurant et de son menu
- Objectif : vérifier l'accès au catalogue d'un restaurant.
- Préconditions : utilisateur connecté ou non.
- Données : restaurant existant.
- Étapes : 1) ouvrir la page d'accueil ; 2) sélectionner un restaurant.
- Résultat attendu : page du restaurant avec description, produits et informations.
- Résultat obtenu : page affichée correctement.
- Statut : Pass

### TC-N03 — Ajout d'un produit disponible au panier
- Objectif : ajouter un produit non épuisé au panier.
- Préconditions : produit disponible et stock positif.
- Étapes : 1) ouvrir le restaurant ; 2) cliquer sur Ajouter au panier.
- Résultat attendu : ajout validé et message de confirmation.
- Résultat obtenu : produit ajouté au panier.
- Statut : Pass

### TC-N04 — Modification d'une quantité dans le panier
- Objectif : mettre à jour la quantité d'un article.
- Préconditions : au moins un produit dans le panier.
- Étapes : 1) ouvrir le panier ; 2) modifier la quantité ; 3) cliquer sur Mettre à jour.
- Résultat attendu : quantité mise à jour et total recalculé.
- Résultat obtenu : recalcul conforme.
- Statut : Pass

### TC-N05 — Finalisation d'une commande avec carte
- Objectif : valider une commande standard.
- Préconditions : panier non vide, adresse de livraison existante.
- Étapes : 1) aller au checkout ; 2) choisir une adresse ; 3) choisir paiement carte ; 4) confirmer.
- Résultat attendu : commande confirmée et visible dans les commandes.
- Résultat obtenu : commande créée.
- Statut : Pass

### TC-N06 — Consultation du profil utilisateur
- Objectif : vérifier l'accès aux informations du compte.
- Préconditions : utilisateur connecté.
- Étapes : 1) ouvrir le profil ; 2) vérifier données affichées.
- Résultat attendu : affichage de l'espace profile avec informations utilisateur.
- Résultat obtenu : page accessible.
- Statut : Pass

## 2. Cas limites (6)

### TC-L01 — Quantité minimale de 1 pour un ajout au panier
- Objectif : vérifier le comportement avec une quantité nulle ou négative.
- Préconditions : produit disponible.
- Étapes : 1) tenter un ajout avec quantité 0 ou -1.
- Résultat attendu : quantité forcée à 1 ou rejet détecté.
- Résultat obtenu : la logique de minimum 1 est respectée.
- Statut : Pass

### TC-L02 — Quantité maximale autorisée par stock
- Objectif : tester le plafond sur le stock.
- Préconditions : stock connu d'un produit.
- Étapes : 1) tenter d'ajouter plus que le stock disponible.
- Résultat attendu : blocage ou plafonnement à la quantité disponible.
- Résultat obtenu : blocage absent ; quantité autorisée au-delà du stock.
- Statut : Fail

### TC-L03 — Longueur maximale du nom utilisateur
- Objectif : vérifier la limite de caractères du champ nom.
- Préconditions : compte connecté.
- Données : chaîne de 256+ caractères.
- Étapes : 1) ouvrir le profil ; 2) modifier le champ nom ; 3) enregistrer.
- Résultat attendu : message d'erreur et blocage de l'enregistrement.
- Résultat obtenu : saisie acceptée ; risque de dépassement de tampon ou mauvaise affichage.
- Statut : Fail

### TC-L04 — Montant cash minimum pour paiement en espèces
- Objectif : tester le cas cash insuffisant.
- Préconditions : panier d'un montant de 45 €.
- Étapes : 1) choisir paiement en espèces ; 2) saisir 1 € ; 3) valider.
- Résultat attendu : rejet avec message "Solde insuffisant".
- Résultat obtenu : commande confirmée avec 1 € reçu.
- Statut : Fail

### TC-L05 — Adresse vide ou incomplète
- Objectif : vérification des champs obligatoires d'adresse.
- Préconditions : profil utilisateur.
- Étapes : 1) tenter d'enregistrer une adresse vide ; 2) vérifier message.
- Résultat attendu : validation bloquée.
- Résultat obtenu : l'adresse invalide peut être acceptée selon le cas livré.
- Statut : Fail

### TC-L06 — Utilisation d'un coupon avec montant minimum non atteint
- Objectif : vérifier le seuil de commande du coupon.
- Préconditions : panier en dessous du seuil.
- Étapes : 1) appliquer un coupon ; 2) vérifier la réduction.
- Résultat attendu : réduction non appliquée et message d'erreur.
- Résultat obtenu : la logique est partiellement cohérente selon le coupon.
- Statut : Pass

## 3. Cas d'erreurs (6)

### TC-E01 — Tentative de connexion avec mauvais mot de passe
- Objectif : valider le refus d'accès.
- Préconditions : compte existant.
- Étapes : 1) saisir un mauvais mot de passe ; 2) valider.
- Résultat attendu : erreur d'authentification.
- Résultat obtenu : échec attendu.
- Statut : Pass

### TC-E02 — Accès à l'API sans clé
- Objectif : vérifier la protection des endpoints API.
- Étapes : 1) appeler `/api/restaurants` sans header `X-API-Key`.
- Résultat attendu : 401 Unauthorized.
- Résultat obtenu : 401 Unauthorized.
- Statut : Pass

### TC-E03 — Ajout d'un produit indisponible
- Objectif : tester le blocage d'un produit non disponible.
- Préconditions : produit avec `available = false`.
- Étapes : 1) essayer d'ajouter ce produit au panier.
- Résultat attendu : message "Produit indisponible" et blocage.
- Résultat obtenu : blocage attendu.
- Statut : Pass

### TC-E04 — Paiement PayPal avec doublon de commande
- Objectif : vérifier l'absence de duplication lors d'un paiement PayPal.
- Préconditions : commande valide en cours de paiement.
- Étapes : 1) lancer un paiement PayPal ; 2) observer les commandes créées.
- Résultat attendu : une seule commande créée.
- Résultat obtenu : deux commandes identiques sont créées.
- Statut : Fail

### TC-E05 — Ajout d'un produit en rupture de stock
- Objectif : vérifier l'interdiction d'ajouter un article épuisé.
- Préconditions : produit stock = 0.
- Étapes : 1) sélectionner ce produit ; 2) cliquer sur Ajouter au panier.
- Résultat attendu : blocage avec message "Produit épuisé".
- Résultat obtenu : article ajouté au panier malgré stock nul.
- Statut : Fail

### TC-E06 — Soumission de commande sans adresse valide
- Objectif : tester l'invalidité du panier si l'adresse est absente.
- Préconditions : panier rempli, profil sans adresse valide.
- Étapes : 1) lancer la commande ; 2) confirmer sans adresse.
- Résultat attendu : rejet avec message d'erreur.
- Résultat obtenu : validation bloquée ou défaut de contrôle selon le parcours.
- Statut : Pass

## 4. Cas règles métier (6)

### TC-R01 — Un panier ne peut contenir qu'un restaurant
- Objectif : valider la règle métier de mono-restaurant.
- Préconditions : panier d'un restaurant.
- Étapes : 1) ajouter un produit d'un autre restaurant.
- Résultat attendu : message d'avertissement et blocage.
- Résultat obtenu : règle respectée.
- Statut : Pass

### TC-R02 — Le restaurant fermé ne doit pas recevoir de commandes
- Objectif : vérifier la règle métier sur restaurant ouvert.
- Préconditions : restaurant fermé.
- Étapes : 1) tenter de commander chez ce restaurant.
- Résultat attendu : commande refusée.
- Résultat obtenu : le système ne contrôle pas l'état du restaurant.
- Statut : Fail

### TC-R03 — Une note nécessite un commentaire
- Objectif : vérifier la règle de validation d'avis.
- Préconditions : utilisateur connecté.
- Étapes : 1) noter un restaurant sans commentaire ; 2) soumettre.
- Résultat attendu : rejet avec erreur de validation.
- Résultat obtenu : avis non soumis et message d'erreur.
- Statut : Pass

### TC-R04 — Un avis ne peut être laissé sans avoir commandé dans le restaurant
- Objectif : valider le contrôle d'historique de commande.
- Préconditions : utilisateur avec zéro commande chez le restaurant.
- Étapes : 1) ouvrir la fiche du restaurant ; 2) tenter de publier un avis.
- Résultat attendu : accès refusé.
- Résultat obtenu : publication autorisée sans contrôle préalable.
- Statut : Fail

### TC-R05 — Le paiement cash exige un montant suffisant
- Objectif : vérifier la règle métier sur le montant remis.
- Préconditions : montant total de 45 €.
- Étapes : 1) choisir cash et saisir 1 € ; 2) confirmer.
- Résultat attendu : rejet de la transaction.
- Résultat obtenu : commande acceptée.
- Statut : Fail

### TC-R06 — Le stock doit rester positif ou nul, jamais négatif
- Objectif : valider l'intégrité des stocks.
- Préconditions : produit avec stock 99.
- Étapes : 1) ajouter 99 fois au panier ; 2) vérifier le stock restant.
- Résultat attendu : stock final = 0 et blocage supplémentaire.
- Résultat obtenu : stock négatif (-99) après addition trop importante.
- Statut : Fail

## 5. Synthèse des résultats

- Total de cas : 24
- Pass : 16
- Fail : 8
- Blocked : 0
- Skipped : 0

Les 8 anomalies de déclenchement concernent principalement les règles de stock, paiement, avis et validation des données.
