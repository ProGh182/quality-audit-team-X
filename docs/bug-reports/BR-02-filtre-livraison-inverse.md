# BR-02 — Filtre « livraison max » retourne l'inverse du résultat attendu

| Champ       | Valeur |
|-------------|--------|
| Sévérité    | 🟠 Haute |
| Priorité    | P1 |
| Statut      | Ouvert |
| Cas associé | CT-M05 |

## Contexte

Le filtre `max_delivery` sur la page d'accueil utilise `>=` au lieu de `<=` dans la requête SQL (`main.py`, ligne ~17). Le résultat affiché est donc l'inverse de ce que l'utilisateur attend.

## Préconditions

- Application lancée
- Au moins 2 restaurants avec des frais de livraison différents

## Étapes de reproduction

1. Aller sur la page d'accueil
2. Renseigner **Livraison max : 2,50 €**
3. Observer les restaurants affichés

## Résultat attendu

Seuls les restaurants avec des frais de livraison **<= 2,50 €** sont affichés.

## Résultat obtenu

Les restaurants avec des frais de livraison **> 2,50 €** sont affichés — résultat inversé.

## Preuve

> 📎 Joindre : capture d'écran des résultats avec le filtre appliqué.

## Correction suggérée

Dans `main.py`, remplacer `>=` par `<=` dans le filtre `max_delivery`.
