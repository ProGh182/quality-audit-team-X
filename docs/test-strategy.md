# Stratégie de test — QuickOrder v3.1

## 1. Objectif

Évaluer la qualité de l'application QuickOrder avant sa mise en production en identifiant les anomalies sur les parcours critiques, l'API REST et les règles métier.

---

## 2. Périmètre

### Dans le périmètre

| Domaine         | Éléments couverts |
|-----------------|-------------------|
| Authentification | Inscription, connexion, déconnexion |
| Catalogue        | Recherche, filtres (catégorie, végétarien, livraison max), tri |
| Panier           | Ajout, modification de quantité, suppression, vidage, règle mono-restaurant |
| Coupons          | Validation, minimum, expiration, plafond de réduction |
| Checkout         | Sélection adresse, modes de paiement (carte, PayPal, espèces), confirmation |
| Commandes        | Historique, détail, annulation, recommander |
| Favoris          | Ajout / suppression |
| Avis             | Soumission, validation note et commentaire |
| Profil           | Mise à jour nom/téléphone, gestion adresses |
| Admin            | Tableau de bord, changement de statut commande |
| API REST         | Tous les endpoints documentés dans Swagger |

### Hors périmètre

- Tests de charge et de performance
- Sécurité avancée (pentest, injection SQL, XSS)
- Compatibilité multi-navigateurs (hors Chrome/Firefox)
- Infrastructure et déploiement en production
- Module de paiement réel (simulé uniquement)

---

## 3. Parcours critiques

| ID  | Parcours                                                      | Importance |
|-----|---------------------------------------------------------------|------------|
| PC1 | Inscription → Connexion → Commande → Confirmation             | Critique   |
| PC2 | Ajout panier → Application coupon → Checkout PayPal           | Critique   |
| PC3 | Recherche restaurant → Filtre → Ajout panier                  | Haute      |
| PC4 | Annulation de commande                                        | Haute      |
| PC5 | API : création de commande avec coupon                        | Haute      |
| PC6 | Admin : mise à jour de statut de commande                     | Moyenne    |

---

## 4. Types de tests

- **Tests fonctionnels** — UI navigateur + DevTools
- **Tests d'API REST** — Swagger / Postman / Bruno
- **Tests aux limites** — valeurs frontières : quantités, montants, longueurs
- **Tests de règles métier** — coupons, stock, restaurant fermé, mono-restaurant
- **Tests d'erreur** — inputs invalides, ressources inexistantes, accès non autorisé

---

## 5. Outils

| Outil        | Usage |
|--------------|-------|
| Chrome / Firefox | Tests UI, DevTools (onglet Network / Console) |
| Swagger (`/docs/`) | Tests API REST |
| Postman / Bruno | Tests API avancés, collections |
| Excel | Suivi des cas de test et bug reports |

---

## 6. Priorisation risque × impact

| Priorité | Critère |
|----------|---------|
| P1 — Critique | Flux de paiement, création de commande, calcul des prix |
| P2 — Haute | Catalogue, filtres, coupons |
| P3 — Moyenne | Avis, favoris, profil |
| P4 — Faible | Cosmétique, contenu statique |
