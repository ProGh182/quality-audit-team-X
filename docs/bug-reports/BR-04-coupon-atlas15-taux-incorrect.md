# BR-04 — Coupon ATLAS15 applique 10 % au lieu de 15 %

| Champ       | Valeur |
|-------------|--------|
| Sévérité    | 🟠 Haute |
| Priorité    | P1 |
| Statut      | Ouvert |
| Cas associé | CT-M04 |

## Contexte

Le coupon `ATLAS15` est présenté à l'utilisateur comme offrant **15 % de réduction**, mais la base de données stocke `discount_percent = 10` (`seed.py`). L'écart de 5 points expose l'entreprise à un litige commercial.

## Préconditions

- Connecté
- Panier avec un sous-total >= 20 €

## Étapes de reproduction

1. Aller sur `/checkout`
2. Saisir le coupon **ATLAS15**
3. Observer la réduction appliquée au total

## Résultat attendu

Réduction de **15 %** appliquée sur le sous-total.

## Résultat obtenu

Réduction de **10 %** appliquée — écart de 5 points avec la promotion affichée.

## Preuve

> 📎 Joindre : capture d'écran du checkout affichant la réduction calculée avec ATLAS15.

## Correction suggérée

Dans `seed.py` et directement en base, mettre `discount_percent = 15` pour le coupon ATLAS15.
