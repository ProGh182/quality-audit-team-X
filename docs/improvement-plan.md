# Plan d'amélioration — QuickOrder v3.1

## Améliorations prioritaires (bloquantes)

| #  | Amélioration                                                                 | Priorité     | Effort | Justification |
|----|------------------------------------------------------------------------------|--------------|--------|---------------|
| A1 | **Corriger le bug PayPal** : supprimer la création du duplicate `Order` dans `checkout.py` et `api.py` | P1 — Critique | Faible | Double facturation client, risque financier et légal immédiat |
| A2 | **Corriger le filtre `max_delivery`** : remplacer `>=` par `<=` dans `main.py` (route index) | P1 — Haute | Faible | Filtre renvoie l'opposé du comportement attendu, UX cassée |
| A3 | **Valider le montant espèces côté serveur** : refuser si `cash_received < total` dans `build_order()` | P1 — Haute | Faible | Perte financière directe si commande espèces acceptée avec montant insuffisant |
| A4 | **Corriger ATLAS15** : mettre `discount_percent` à `15` dans `seed.py` et la base de données | P1 — Haute | Faible | Litige commercial : promotion affichée à 15 % mais appliquée à 10 % |
| A5 | **Vérifier `is_open` au checkout** : bloquer la commande si le restaurant est fermé | P1 — Haute | Faible | Commandes impossibles à honorer créées sur des restaurants fermés |
| A6 | **Exiger une commande préalable pour les avis** : vérifier `user_id` + `restaurant_id` avant d'enregistrer un avis | P2 — Moyenne | Faible | Avis frauduleux possibles, nuisent à la fiabilité des notes |

---

## Améliorations complémentaires (non bloquantes)

| #  | Amélioration                                                                              | Priorité  |
|----|-------------------------------------------------------------------------------------------|-----------|
| B1 | Vérifier le stock (`stock > 0`) avant ajout au panier et avant checkout                   | P2 — Haute |
| B2 | Recalculer le `subtotal` côté serveur dans `/coupons/validate` (ne pas faire confiance au client) | P2 — Haute |
| B3 | Bloquer les transitions de statut impossibles en admin (ex. `delivered` → `confirmed`)    | P2 — Moyenne |
| B4 | Étendre la recherche à la description des restaurants (UI et API)                         | P3 — Faible |
| B5 | Afficher un badge « Fermé » sur les restaurants avec `is_open=False` dans la liste        | P3 — Faible |

---

## Ordre de correction recommandé

```
A1 → A2 → A3 → A4 → A5 → B1 → B2 → A6 → B3 → B4 → B5
```

Après correction des items A1 à A5, une **campagne de revalidation** doit être menée sur les cas CT-M02, CT-M03, CT-M04, CT-M05 et CT-M06 avant toute décision de Go.
