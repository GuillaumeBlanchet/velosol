# A3

## Ajout d'une pièce à l'inventaire

### 1. Fil d'Arianne
Inventory -> Products -> New
### 2. Notes
Prendre soin de décocher "Can be sold", car vous ne produisez pas les pièces.

- Mettre le nom dans le titre (e.g. "Handle Bar Bixi 3.0 Black ano")
- Mettre votre code (e.g. "V00001") dans le champ barcode
- Entrez le coût de la pièce dans "cost" (e.g. 28$)
- Utiliser le "Add Properties" pour ajouter les champs Manufacturer & Manufacturer Reference manquants (et tout autre champ pertinent)
- Allez dans l'onglet "Purchase" de la pièce pour rentrer le fournisseur ("vendor").


## Modification d'une pièce à l'inventaire

### 1. Fil d'Arianne
Inventory -> Products 

### 2. Notes
Vous pouvez sélectionner vos pièces et les modifiers là.

## Suppression d'une pièce à l'inventaire
On peut bouger les pièces de l'inventaire de plusieurs façons:

### 1. Inventory -> Operations -> Adjustment / Physical inventory

C'est comme son nom l'indique un ajustement d'inventaire manuel. On remet les quantités aux bonnes valeurs
qu'on observe dans l'entrepôt.

### 2. Inventory -> Operations -> Internal (Internal Transfers)

On peut bouger les pièces entre les entrepôts prédéfinis dans "Configuration -> Warehouses"