# Matrice des risques — QuickOrder v3.1

Risques identifiés à partir de l'analyse du code source avant exécution de la campagne.

---

## Matrice

| ID  | Risque                                                                 | Probabilité | Impact   | Priorité | Bug associé |
|-----|------------------------------------------------------------------------|-------------|----------|----------|-------------|
| R1  | PayPal duplique la commande (bug intentionnel dans `orders.py`)        | Certaine    | Critique | **P1**   | BR-01       |
| R2  | Filtre `max_delivery` inversé (`>=` au lieu de `<=`) dans `main.py`   | Certaine    | Haute    | **P1**   | BR-02       |
| R3  | Paiement espèces accepté avec montant inférieur au total               | Certaine    | Haute    | **P1**   | BR-03       |
| R4  | Coupon ATLAS15 configuré à 10 % au lieu de 15 % dans `seed.py`        | Certaine    | Haute    | **P1**   | BR-04       |
| R5  | Commande possible sur restaurant fermé (`is_open` non vérifié)         | Certaine    | Haute    | **P1**   | BR-05       |
| R6  | Produit avec `stock=0` ajoutable au panier (vérification absente)      | Certaine    | Haute    | **P1**   | BR-06       |
| R7  | Avis soumis sans commande préalable dans le restaurant                 | Certaine    | Moyenne  | **P2**   | BR-07       |
| R8  | API `/coupons/validate` — subtotal fourni par le client, non recalculé | Certaine    | Haute    | **P1**   | BR-08       |
| R9  | Transitions de statut admin impossibles acceptées (ex. livré → confirmé) | Probable  | Moyenne  | **P2**   | —           |
| R10 | Recherche UI et API indexée sur le nom uniquement (pas la description) | Certaine    | Faible   | **P3**   | —           |

---

## Légende

| Probabilité | Définition |
|-------------|------------|
| Certaine    | Confirmé dans le code source |
| Probable    | Comportement attendu vu l'implémentation |
| Possible    | À vérifier lors de l'exécution |

| Impact   | Définition |
|----------|------------|
| Critique | Bloque un flux de paiement ou crée une incohérence de données majeure |
| Haute    | Affecte directement l'expérience ou le chiffre d'affaires |
| Moyenne  | Dégradation fonctionnelle sans impact financier immédiat |
| Faible   | Gêne mineure pour l'utilisateur |
