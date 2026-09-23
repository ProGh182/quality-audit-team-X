# Rapport d'exécution — Campagne QuickOrder v3.1

## Informations générales

| Champ              | Valeur |
|--------------------|--------|
| Application        | QuickOrder v3.1 |
| URL                | http://127.0.0.1:5000 |
| Swagger            | http://127.0.0.1:5000/docs/ |
| Outils utilisés    | Navigateur (Chrome), DevTools, Swagger, Postman |
| Compte principal   | alice@example.com / Password123! |

---

## Synthèse des résultats

| Métrique              | Valeur |
|-----------------------|--------|
| Total cas de test     | 24     |
| ✅ Pass               | 19     |
| ❌ Fail               | 5      |
| 🔒 Blocked            | 0      |
| ⏭️ Skipped            | 0      |
| Taux de réussite      | 79 %   |
| Bugs critiques (P1)   | 1      |
| Bugs haute sév. (P1)  | 5      |
| Bugs moyenne sév. (P2)| 1      |

---

## Résultats par cas de test

| ID      | Titre                              | Type    | Statut  |
|---------|------------------------------------|---------|---------|
| CT-N01  | Connexion réussie                  | Nominal | ✅ Pass |
| CT-N02  | Inscription nouvel utilisateur     | Nominal | ✅ Pass |
| CT-N03  | Ajout produit au panier            | Nominal | ✅ Pass |
| CT-N04  | Commande complète (carte)          | Nominal | ✅ Pass |
| CT-N05  | Application coupon valide          | Nominal | ✅ Pass |
| CT-N06  | API GET /restaurants               | Nominal | ✅ Pass |
| CT-L01  | Quantité produit = 1 (minimum)     | Limite  | ✅ Pass |
| CT-L02  | Quantité = 20 (maximum API)        | Limite  | ✅ Pass |
| CT-L03  | Quantité = 21 (hors limite API)    | Limite  | ✅ Pass |
| CT-L04  | Coupon exactement au minimum       | Limite  | ✅ Pass |
| CT-L05  | Coupon sous le minimum (19,99 €)   | Limite  | ✅ Pass |
| CT-L06  | Mot de passe à 8 caractères        | Limite  | ✅ Pass |
| CT-E01  | Connexion mauvais mot de passe     | Erreur  | ✅ Pass |
| CT-E02  | API sans clé API                   | Erreur  | ✅ Pass |
| CT-E03  | API clé incorrecte                 | Erreur  | ✅ Pass |
| CT-E04  | Restaurant inexistant (API)        | Erreur  | ✅ Pass |
| CT-E05  | Commande API quantité 0            | Erreur  | ✅ Pass |
| CT-E06  | Annuler commande déjà livrée       | Erreur  | ✅ Pass |
| CT-M01  | Panier mono-restaurant             | Métier  | ✅ Pass |
| CT-M02  | PayPal — doublon commande          | Métier  | ❌ Fail |
| CT-M03  | Espèces montant insuffisant        | Métier  | ❌ Fail |
| CT-M04  | Coupon ATLAS15 — taux incorrect    | Métier  | ❌ Fail |
| CT-M05  | Filtre livraison max UI            | Métier  | ❌ Fail |
| CT-M06  | Avis sans commande                 | Métier  | ❌ Fail |

---

## Cas en échec — résumé

| ID     | Résultat attendu                          | Résultat obtenu                                          | Bug    |
|--------|-------------------------------------------|----------------------------------------------------------|--------|
| CT-M02 | 1 seule commande créée (PayPal)           | 2 commandes identiques créées simultanément              | BR-01  |
| CT-M03 | Refus si cash_received < total            | Commande acceptée avec 1 € pour un total de ~15 €        | BR-03  |
| CT-M04 | Réduction de 15 % avec ATLAS15            | Réduction de 10 % appliquée                              | BR-04  |
| CT-M05 | Restaurants avec livraison <= 2,50 €      | Restaurants avec livraison > 2,50 € affichés             | BR-02  |
| CT-M06 | Avis refusé sans commande préalable       | Avis accepté sans vérification de commande               | BR-07  |

---

## Principaux risques confirmés

| Réf.  | Risque                                              | Impact   |
|-------|-----------------------------------------------------|----------|
| BR-01 | PayPal duplique chaque commande → double facturation | Critique |
| BR-02 | Filtre livraison inversé → résultats erronés         | Haute    |
| BR-03 | Paiement espèces insuffisant accepté → perte financière | Haute |
| BR-04 | Coupon ATLAS15 mal configuré → litige commercial     | Haute    |
| BR-05 | Commande sur restaurant fermé → commande non honorable | Haute  |
| BR-08 | Subtotal manipulable → mapping des plafonds coupons  | Haute    |

---

## Recommandation

> ❌ **NO-GO**
>
> L'application présente **6 anomalies de priorité P1** affectant directement les flux de paiement, le calcul des prix et la gestion des commandes. Ces bugs sont incompatibles avec une mise en production. Une correction et une campagne de revalidation sont requises avant toute livraison.
