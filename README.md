# Analyse des Ventes d'une Pizzeria — Dashboard Power BI

**Auteur :** Yacine Yefsah  
**Période analysée :** Janvier 2015 – Décembre 2015  
**Outil :** Microsoft Power BI  
**Type de projet :** Analyse décisionnelle — Business Intelligence

---

## Contexte et Problématique

Une pizzeria souhaite mieux comprendre ses performances commerciales sur l'année 2015 afin d'optimiser son offre, ses ressources humaines et sa stratégie de vente.

La direction dispose de quatre tables de données brutes couvrant l'ensemble des commandes de l'année. Elle souhaite transformer ces données en indicateurs clairs et actionnables pour prendre des décisions éclairées.

L'objectif de ce projet est de concevoir un dashboard Power BI permettant de répondre aux principales questions métier, d'identifier les tendances et de formuler des recommandations concrètes.

---

## Questions Métier Traitées

1. Quel est le **chiffre d'affaires total** généré sur l'année 2015 ?
2. Combien de **commandes** ont été passées et combien de **pizzas** ont été vendues ?
3. Quelle est la **valeur moyenne d'une commande** ?
4. Quelles sont les **pizzas les plus vendues** et les **moins vendues** ?
5. Quelles sont les **catégories** de pizzas qui génèrent le plus de revenus (Chicken, Classic, Supreme, Veggie) ?
6. Quelle **taille de pizza** est la plus demandée par les clients ?
7. Quels sont les **jours de la semaine** les plus chargés en commandes ?
8. Quels sont les **mois** avec le plus de commandes sur l'année ?
9. À quelles **heures** de la journée le volume de commandes est-il le plus élevé ?
10. Y a-t-il des **pizzas à faible performance** qui pourraient être retirées de la carte ?

---

## Description des Fichiers

Le dataset est composé de quatre fichiers CSV reliés entre eux par des clés étrangères.

### `orders.csv` — 21 350 commandes
Contient une ligne par commande avec sa date et son heure de passage. C'est la table centrale des transactions.

| Colonne | Description |
|---|---|
| `order_id` | Identifiant unique de la commande |
| `date` | Date de la commande (format YYYY-MM-DD) |
| `time` | Heure de la commande (format HH:MM:SS) |

### `order_details.csv` — 48 620 lignes
Contient le détail de chaque commande : quelle pizza a été commandée, en quelle quantité. Une commande peut contenir plusieurs lignes (plusieurs pizzas différentes).

| Colonne | Description |
|---|---|
| `order_details_id` | Identifiant unique de la ligne de détail |
| `order_id` | Référence à la commande (clé étrangère → `orders.csv`) |
| `pizza_id` | Référence à la pizza commandée (clé étrangère → `pizzas.csv`) |
| `quantity` | Quantité commandée |

### `pizzas.csv` — 96 variantes
Contient les déclinaisons de chaque pizza par taille (S, M, L, XL, XXL) avec le prix correspondant.

| Colonne | Description |
|---|---|
| `pizza_id` | Identifiant unique de la pizza (type + taille) |
| `pizza_type_id` | Référence au type de pizza (clé étrangère → `pizza_types.csv`) |
| `size` | Taille de la pizza : S, M, L, XL ou XXL |
| `price` | Prix unitaire en dollars |

### `pizza_types.csv` — 33 types de pizzas
Contient le catalogue de pizzas avec leur nom, leur catégorie et leurs ingrédients.

| Colonne | Description |
|---|---|
| `pizza_type_id` | Identifiant unique du type de pizza |
| `name` | Nom commercial de la pizza |
| `category` | Catégorie : Chicken, Classic, Supreme ou Veggie |
| `ingredients` | Liste des ingrédients |

---

## Modèle de Données

Les quatre tables sont reliées selon le schéma suivant :

```
orders (order_id) ──── order_details (order_id, pizza_id) ──── pizzas (pizza_id, pizza_type_id) ──── pizza_types (pizza_type_id)
```

---

## Résultats Clés

### Indicateurs Globaux

| Indicateur | Valeur |
|---|---|
| Chiffre d'affaires total | **817 860 $** |
| Nombre de commandes | **21 350** |
| Nombre de pizzas vendues | **49 574** |
| Valeur moyenne par commande | **~38,3 $** |

### Pizzas les Plus Vendues (Top 5)

| Pizza | Quantité vendue |
|---|---|
| The Big Meat Pizza (S) | 1 914 |
| The Thai Chicken Pizza (L) | 1 410 |
| The Five Cheese Pizza (L) | 1 409 |
| The Four Cheese Pizza (L) | 1 316 |
| The Classic Deluxe Pizza (M) | 1 181 |

### Pizzas les Moins Vendues (Bottom 3)

| Pizza | Quantité vendue |
|---|---|
| The Greek Pizza (XXL) | 28 |
| The Green Garden Pizza (L) | 95 |
| The Chicken Alfredo Pizza (S) | 96 |

### Pics d'Activité

**Heures de pointe :** 12h (2 520 commandes), 13h (2 455 commandes), 18h (2 399 commandes) — deux créneaux clairs : déjeuner et dîner.

**Mois les plus chargés :** Juillet (1 935), Mai (1 853), Mars (1 840).

**Mois les plus calmes :** Septembre (1 661), Octobre (1 646), Février (1 685).

---

## Recommandations

**1. Renforcer les ressources aux heures de pointe**
Les créneaux 12h–13h et 18h–19h concentrent le gros du volume. Il est conseillé d'ajuster les équipes en cuisine et en livraison sur ces plages horaires pour maintenir la qualité de service.

**2. Valoriser les best-sellers dans la communication**
The Big Meat (S) et les pizzas fromage en grande taille sont les locomotives de l'offre. Les mettre en avant dans les promotions et sur les supports de communication peut amplifier encore leur performance.

**3. Réévaluer les pizzas à très faible vente**
The Greek XXL (28 ventes sur un an), The Green Garden L et The Chicken Alfredo S génèrent très peu de chiffre d'affaires. Il convient soit de les supprimer de la carte, soit de les retravailler (recette, prix, visibilité).

**4. Lancer des offres ciblées en période creuse**
Les mois de septembre, octobre et février affichent les plus faibles volumes. Des promotions spécifiques (menus famille, offres groupées) pourraient dynamiser les ventes sur ces périodes.

**5. Analyser la rentabilité par catégorie**
Une analyse complémentaire des marges par catégorie (Chicken, Classic, Supreme, Veggie) permettrait d'identifier les gammes les plus rentables, au-delà du simple volume.

---

## Fichiers du Projet

```
pizza-sales-analysis/
│
├── Yacine_Yefsah_22310440.pbix   # Dashboard Power BI complet
├── data/
│   ├── orders.csv                 # Table des commandes
│   ├── order_details.csv          # Détail des commandes
│   ├── pizzas.csv                 # Catalogue pizzas + tailles + prix
│   └── pizza_types.csv            # Types de pizzas + catégories + ingrédients
└── README.md
```
