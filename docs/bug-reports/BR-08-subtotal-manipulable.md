# BR-08 — API /coupons/validate — subtotal client non recalculé côté serveur

| Champ       | Valeur |
|-------------|--------|
| Sévérité    | 🟠 Haute |
| Priorité    | P1 |
| Statut      | Ouvert |
| Cas associé | — |

## Contexte

L'endpoint `POST /coupons/validate` fait confiance au `subtotal` envoyé par le client sans le recalculer côté serveur (`api.py`). Un `subtotal` gonflé artificiellement permet de calculer la réduction maximale d'un coupon, exposant ainsi les plafonds de remise.

## Préconditions

- Clé API configurée dans Swagger (`quickorder-demo-key`)
- Coupon `WELCOME10` actif

## Étapes de reproduction

1. Dans Swagger, appeler `POST /coupons/validate`
2. Envoyer le body suivant :
   ```json
   {
     "code": "WELCOME10",
     "subtotal": 99999
   }
   ```
3. Observer la réduction retournée

## Résultat attendu

La réduction est calculée sur le vrai sous-total du panier de l'utilisateur, pas sur la valeur envoyée par le client.

## Résultat obtenu

La réduction est calculée sur `99999 €` — `discount` plafonné à `8,00 €`. Le client peut ainsi déterminer le plafond exact de n'importe quel coupon en manipulant le `subtotal`.

## Preuve

> 📎 Joindre : copie JSON de la réponse Swagger avec `subtotal: 99999`.

## Correction suggérée

Dans `api.py`, recalculer le `subtotal` réel à partir du panier de l'utilisateur authentifié, sans utiliser la valeur fournie par le client.
