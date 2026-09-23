# BR-03 — Paiement espèces accepté avec montant inférieur au total

| Champ       | Valeur |
|-------------|--------|
| Sévérité    | 🟠 Haute |
| Priorité    | P1 |
| Statut      | Ouvert |
| Cas associé | CT-M03 |

## Contexte

La commande est confirmée même si le montant espèces fourni (`cash_received`) est inférieur au total dû. Un `change_due` négatif est enregistré en base de données (`orders.py`).

## Préconditions

- Connecté, panier non vide
- Total du panier : ~15 €

## Étapes de reproduction

1. Aller sur `/checkout`
2. Sélectionner le mode de paiement **Espèces**
3. Saisir `cash_received = 1`
4. Confirmer la commande

## Résultat attendu

La commande est refusée avec le message : *« Montant insuffisant »*.

## Résultat obtenu

La commande est confirmée. Un `change_due` négatif est enregistré en base de données.

## Preuve

> 📎 Joindre : capture d'écran du détail de la commande confirmée avec `cash_received = 1 €`.

## Correction suggérée

Dans `build_order()`, ajouter une vérification : refuser si `cash_received < total`.
