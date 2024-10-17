# Nettoyage des Données - Projet "Target Brilliance"

## Description
Ce projet consiste à nettoyer un ensemble de données sur les commandes en ligne pour les préparer à une analyse plus approfondie. Le nettoyage a été réalisé en deux étapes : d'abord avec **Excel**, puis avec **Python** pour automatiser et finaliser le processus de manière plus efficace.

## Fichier de Données
- **Nom du fichier** : `orders.csv`
- **Colonnes principales** :
  - `order_purchase_timestamp` : Date et heure d'achat de la commande.
  - `order_status` : Statut de la commande (livré, en cours, inconnu, etc.).
  - `order_delivered_customer_date` : Date à laquelle la commande a été livrée au client.

## Étapes de Nettoyage

### 1. Nettoyage avec **Excel** :
L'objectif initial était de comprendre les données et de réaliser une première phase de nettoyage. Voici les actions effectuées dans Excel :
  - **Vérification des dates manquantes** : 
    - En activant un filtre sur la colonne `order_purchase_timestamp`, j'ai rapidement identifié et supprimé les lignes avec des dates manquantes.
  - **Suppression des commandes avec un statut inconnu** :
    - J'ai appliqué un filtre sur la colonne `order_status` pour identifier et supprimer toutes les commandes dont le statut était "inconnu".

L'utilisation d'Excel a permis un premier tri visuel et une compréhension rapide des anomalies dans les données.

### 2. Automatisation du Nettoyage avec **Python** :
Après avoir effectué une première phase dans Excel, j'ai automatisé le processus avec Python pour traiter efficacement l'ensemble du fichier et garantir l'absence d'erreurs humaines. Voici les étapes réalisées avec Python :
  - **Vérification des Dates Completes** :
    - Avec la librairie **Pandas**, j'ai vérifié que toutes les commandes contenaient une date d'achat valide (`order_purchase_timestamp`). Les commandes sans date ont été supprimées.
  - **Suppression des Statuts Inconnus** :
    - Toutes les commandes avec un statut "inconnu" dans la colonne `order_status` ont été supprimées automatiquement via le script Python.
  - **Vérification de la Cohérence des Dates de Livraison** :
    - Les commandes où la date de livraison (`order_delivered_customer_date`) était antérieure à la date d'achat ont été supprimées pour assurer la cohérence des données.

### Exemple de code Python :
```python
import pandas as pd

# Charger le fichier CSV
df = pd.read_csv('orders.csv')

# Suppression des lignes avec des dates d'achat manquantes
df_cleaned = df.dropna(subset=['order_purchase_timestamp'])

# Suppression des commandes avec un statut inconnu
df_cleaned = df_cleaned[df_cleaned['order_status'] != 'unknown']

# Suppression des commandes avec des incohérences entre les dates d'achat et de livraison
df_cleaned = df_cleaned[df_cleaned['order_delivered_customer_date'] >= df_cleaned['order_purchase_timestamp']]

# Sauvegarder le fichier nettoyé
df_cleaned.to_csv('cleaned_orders.csv', index=False)
```

## Utilisation

### Prérequis
- Excel (pour la première phase)
- Python 3.x
- Pandas (librairie Python pour le traitement des données)

### Installation
Pour installer la librairie Pandas, exécutez la commande suivante :

```bash
pip install pandas
```

### Exécution du Script Python
1. Clonez ce dépôt ou téléchargez le fichier `orders.csv`.
2. Exécutez le script Python de nettoyage avec la commande suivante :

```bash
python nettoyage_donnees.py
```

Cela générera un fichier nettoyé `cleaned_orders.csv`.

## Conclusion
Grâce à une première exploration et un nettoyage manuel avec **Excel**, suivis d'un traitement automatisé avec **Python**, les données sont maintenant prêtes pour une analyse plus approfondie. Ce processus a permis de s'assurer que les dates sont cohérentes, les statuts valides, et que les données ne contiennent aucune information erronée ou incomplète.

## Contributeurs
*- **(Taibi El Yakouti) [@xdweb](https://www.linkedin.com/in/xdweb)**, : Nettoyage des données, développement du script Python et rédaction de ce README.*