# BR-07 — Avis restaurant soumis sans commande préalable

| Champ       | Valeur |
|-------------|--------|
| Sévérité    | 🟡 Moyenne |
| Priorité    | P2 |
| Statut      | Ouvert |
| Cas associé | CT-M06 |

## Contexte

La route `POST /restaurant/<id>/review` n'exige pas que l'utilisateur ait passé une commande dans ce restaurant (`shop.py`). N'importe quel utilisateur connecté peut soumettre un avis, ce qui nuit à la fiabilité des notes.

## Préconditions

- Connecté en tant qu'alice
- Restaurant choisi sans commande passée par alice dans ce restaurant

## Étapes de reproduction

1. Aller sur la page d'un restaurant sans avoir commandé
2. Soumettre un avis (note : 4, commentaire quelconque)
3. Observer le résultat

## Résultat attendu

L'avis est refusé avec le message : *« Vous devez avoir commandé pour laisser un avis »*.

## Résultat obtenu

L'avis est accepté et enregistré sans vérification de commande préalable.

## Preuve

> 📎 Joindre : capture d'écran de la confirmation de soumission de l'avis.

## Correction suggérée

Dans `shop.py`, avant d'enregistrer l'avis, vérifier qu'il existe une commande avec `user_id` + `restaurant_id` au statut `delivered` ou `completed`.
