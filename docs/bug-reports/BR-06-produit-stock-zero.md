# BR-06 — Produit avec stock = 0 ajoutable au panier

| Champ       | Valeur |
|-------------|--------|
| Sévérité    | 🟠 Haute |
| Priorité    | P1 |
| Statut      | Ouvert |
| Cas associé | — |

## Contexte

La route `/cart/add` ne vérifie pas le stock du produit, uniquement sa disponibilité booléenne (`available`). Un produit avec `stock = 0` et `available = True` peut donc être ajouté au panier sans avertissement (`shop.py`).

## Préconditions

- Produit avec `stock = 0` et `available = True` dans la base de données
- Connecté

## Étapes de reproduction

1. Identifier un produit avec `stock = 0`
2. Tenter de l'ajouter au panier via `/cart/add/{id}`
3. Observer le comportement

## Résultat attendu

Message *« Produit en rupture de stock »* ou blocage de l'ajout.

## Résultat obtenu

Le produit est ajouté au panier sans aucun avertissement.

## Preuve

> 📎 Joindre : capture d'écran du panier affichant le produit en rupture de stock.

## Correction suggérée

Dans `shop.py`, ajouter une vérification `product.stock > 0` dans la route `/cart/add` avant d'autoriser l'ajout.
