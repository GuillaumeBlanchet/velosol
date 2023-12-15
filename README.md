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
- Allez dans l'onglet "Purchase" de la pièce pour rentrer le fournisseur ("vendor") 
et le prix (important pour l'automatisation des seuils minimaux d'inventaire voir section [A4 - Être informé d’une baisse d’inventaire sous seuil](#A4---Être-informé-d’une-baisse-d’inventaire-sous-seuil))


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

On peut bouger les pièces entre les entrepôts prédéfinis dans "Configuration -> Warehouses".

#### Barcode

Avec le gun, il suffit de scanner l'opération "Internal transfers" sous

Configurations -> Settings -> Barcode -> "Print barcode commands & operation types"

### 3. Inventory -> Operations -> Scrap

On peut déclarer des pièces comme étant hors d'usage (scrap).

#### Barcode

Avec le gun, il suffit de scanner l'opération "Scrap" sous 

Configurations -> Settings -> Barcode -> "Print barcode commands & operation types"

# A4 - Être informé d’une baisse d’inventaire sous seuil

## 1. Fil d'Arianne
Configurations -> Reordering rules -> New (raccourci également dispo directement sur la pièce)

## 2. Notes

- Prendre la route "Buy" pour indiquer que c'est une pièce achetée et non produite.
- Indiquer la quantité min et max (seuils d'inventaire);
- Remarquez que la règle est définie par entrepôt;
- Automatiquement, la quantité "To Order" sera mis à jour selon votre inventaire actuel. C'est ici que vous pouvez être informé 
de vos baisses et projections d'inventaires (il n'y a pas de système de notifications pour ça en tant que tel, on assume qu'Odoo est
votre plateforme de gestion d'inventaire et non votre boîte courriel ou vos SMS).

# A5 - Créer une demande d'achat automatiquement d'une pièce en fonction des seuils

## 1. Fil d'Arianne
Purchase -> Request for quotation

## 2. Notes
Un "Purchase -> Request for quotation" sera automatiquement créé chaque fois que le seuil minimal sera atteint 
Le seuil des stocks sont seulement vérifé chaque 24h par le "scheduler" d'Odoo. Vous pouvez déclencher une synchronisation 
du scheduler manuellement si vous ne voulez pas attendre 24h pour voir apparaître votre "Request for quotation".
Pour ce faire, vous devez activer le mode "developer":

Settings -> General Settings -> Developer Tools -> Activate the developer mode

Une fois ceci fait, vous allez voir apparaître l'opération "Run Scheduler" ici:

Inventory -> Operations -> Run Scheduler.

Vous verrez apparaître votre "Purchase -> Request for quotation" avec le prix total de la commande.
Si vous l'ouvrez, vous pourrez confirmer la commande en cliquant sur "Confirm Order". De là, vous pouvez
envoyer la commande au fournisseur par email en cliquant sur "Send by PO Email".

# A6 - Créer une commande de pièces par fournisseur

## 1. Fil d'Arianne

Purchase -> Request for quotation

## 2. Notes

Si plusieurs pièces sont à commander chez le même fournisseur lorsque le scheduler roule (grâce au reordering rules), Odoo va automatiquement
créer une request for quotation par fournisseur pour l'ensemble des pièces.

Si un Request for quotation existe et qu'une autre pièce du même fournisseur atteint son seuil minimal, Odoo va
ajouter la pièce à la request for quotation existante automatiquement.

# A7 - Recevoir les pièces commandées

## 1. Fil d'Arianne

Barcode -> Scan -> Scan warehouse receipts (Configuration -> Print barcode commands & operation types) -> Scan pièces

## 2. Notes

- Pour l'instant, j'ai mis votre numéro V000XX dans le champ barcode, mais comme vous le constaterez, si vous ne changer
pas de fournisseur, il peut être pratique de mettre le code à barre du fournisseur dans ce champ.
- Une fois le picking de toutes les pièces complété, vous pouvez cliquer sur "Validate" pour confirmer la réception des pièces.
- Si vous scanner le code à barre du dessus, la quantité reçue sera automatiquement inscrite (e.g. 200 pièces). Si vous
scanner le code à barre de la pièce, la quantité reçue sera 1 et vous pourrez ensuite la modifier manuellement. Pratique
lors des réceptions partielles.
