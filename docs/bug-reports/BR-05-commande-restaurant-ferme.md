# BR-05 — Commande possible sur un restaurant fermé

| Champ       | Valeur |
|-------------|--------|
| Sévérité    | 🟠 Haute |
| Priorité    | P1 |
| Statut      | Ouvert |
| Cas associé | — |

## Contexte

La route `/checkout` ne vérifie pas `restaurant.is_open` avant de valider la commande (`orders.py`). Il est donc possible de passer une commande sur un restaurant fermé, ce qui génère des commandes impossibles à honorer.

## Préconditions

- Restaurant avec `is_open = False`
- Panier non vide avec un produit de ce restaurant

## Étapes de reproduction

1. Ajouter un produit d'un restaurant fermé au panier
2. Aller sur `/checkout`
3. Confirmer la commande

## Résultat attendu

La commande est refusée avec le message : *« Restaurant actuellement fermé »*.

## Résultat obtenu

La commande est confirmée malgré le restaurant fermé.

## Preuve

> 📎 Joindre : capture d'écran du détail de la commande confirmée sur un restaurant fermé.

## Correction suggérée

Dans la route checkout (`orders.py`), ajouter une vérification `restaurant.is_open` avant de créer la commande.
