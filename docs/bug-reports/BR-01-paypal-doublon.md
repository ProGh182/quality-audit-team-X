# BR-01 — PayPal crée deux commandes identiques

| Champ       | Valeur |
|-------------|--------|
| Sévérité    | 🔴 Critique |
| Priorité    | P1 |
| Statut      | Ouvert |
| Cas associé | CT-M02 |

## Contexte

Lors d'un paiement PayPal, le checkout crée deux `Order` distincts avec les mêmes articles. Bug confirmé dans `orders.py`.

## Préconditions

- Connecté en tant qu'alice (`alice@example.com / Password123!`)
- Panier avec au moins un produit
- Adresse de livraison existante

## Étapes de reproduction

1. Ajouter un produit au panier
2. Aller sur `/checkout`
3. Sélectionner le mode de paiement **PayPal**
4. Confirmer la commande
5. Aller sur `/orders`

## Résultat attendu

Une seule commande créée dans l'historique.

## Résultat obtenu

Deux commandes identiques apparaissent dans l'historique des commandes.

## Preuve

> 📎 Joindre : capture d'écran de `/orders` montrant les 2 commandes, ou vidéo du flux complet.

## Correction suggérée

Supprimer la création du duplicate `Order` dans la route PayPal de `checkout.py` et `api.py`.
