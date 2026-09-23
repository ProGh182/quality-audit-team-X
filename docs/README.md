<<<<<<< HEAD
# Audit Qualité — QuickOrder v3.1

Rapport complet de la campagne d'audit qualité menée sur **QuickOrder**, une plateforme de livraison de repas, avant sa mise en production.

## Contexte

L'application est développée et fonctionnelle. Notre mission est d'**évaluer sa qualité**, identifier les anomalies et déterminer si elle peut être mise en production.

- **Application** : http://127.0.0.1:5000
- **Swagger** : http://127.0.0.1:5000/docs/
- **Clé API** : `quickorder-demo-key`

## Comptes de test

| Rôle  | Email                     | Mot de passe   |
|-------|---------------------------|----------------|
| Client | alice@example.com        | Password123!   |
| Client | bob@example.com          | Password123!   |
| Admin  | admin@quickorder.local   | Admin123!      |

## Structure du repo

```
quality-audit-team-X/
├── README.md
├── docs/
│   ├── test-strategy.md       # Stratégie de test
│   ├── risk-matrix.md         # Matrice des risques
│   ├── test-cases.xlsx        # Cas de test + campagne + analyse
│   ├── execution-report.md    # Rapport d'exécution de la campagne
│   ├── improvement-plan.md    # Plan d'amélioration
│   └── bug-reports/
│       ├── BR-01-paypal-doublon.md
│       ├── BR-02-filtre-livraison-inverse.md
│       ├── BR-03-especes-montant-insuffisant.md
│       ├── BR-04-coupon-atlas15-taux-incorrect.md
│       ├── BR-05-commande-restaurant-ferme.md
│       ├── BR-06-produit-stock-zero.md
│       ├── BR-07-avis-sans-commande.md
│       └── BR-08-subtotal-manipulable.md
```

## Résultats de la campagne

| Métrique             | Valeur |
|----------------------|--------|
| Total cas de test    | 24     |
| Pass                 | 19     |
| Fail                 | 5      |
| Blocked              | 0      |
| Skipped              | 0      |
| Taux de réussite     | 79 %   |
| Bugs critiques       | 1      |
| Bugs haute sévérité  | 6      |
| Bugs moyenne sévérité| 1      |

## Recommandation

> ❌ **NO-GO** — 6 anomalies bloquantes (P1) non corrigées. La mise en production est impossible en l'état.
=======
# quality-audit-team-X
>>>>>>> c0a5efbed2070a8a530e88c2a385ba1adf6c1175
