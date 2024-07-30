Si vous avez un fichier `nftables` existant qui est un script ASCII, vous pouvez le modifier pour inclure les règles souhaitées. Voici comment procéder :

### Étape 1 : Vérifier et éditer le fichier existant

1. Ouvrez le fichier `nftables` pour l'éditer :

   ```bash
   sudo nano /etc/nftables.conf
   ```

2. Ajoutez les règles suivantes pour bloquer toutes les communications :

   ```nft
   flush ruleset

   table inet filter {
       chain input {
           type filter hook input priority 0; policy drop;
       }
       chain forward {
           type filter hook forward priority 0; policy drop;
       }
       chain output {
           type filter hook output priority 0; policy drop;
       }
   }
   ```

   Enregistrez le fichier et quittez l'éditeur (Ctrl+O pour enregistrer, puis Ctrl+X pour quitter).

### Étape 2 : Appliquer les règles NFTables

Pour appliquer les règles NFTables, vous devez charger le fichier de configuration :

```bash
sudo nft -f /etc/nftables.conf
```

### Étape 3 : Activer NFTables au démarrage

Assurez-vous que le service NFTables est activé pour démarrer au démarrage du système :

```bash
sudo systemctl enable nftables
```

### Étape 4 : Redémarrer le service NFTables

Redémarrez le service NFTables pour appliquer les nouvelles règles :

```bash
sudo systemctl restart nftables
```

### Remarque importante
Cette configuration bloquera **toutes** les communications entrantes, sortantes et de transit. Cela inclut les connexions SSH, ce qui pourrait vous empêcher d'accéder à distance à votre serveur. Assurez-vous que vous avez un accès physique ou un autre moyen d'accéder au serveur pour annuler ces règles si nécessaire.

### Vérifier les règles actuellement appliquées
sudo nft list ruleset

<img width="572" alt="Capture d’écran 2024-07-30 à 15 18 39" src="https://github.com/user-attachments/assets/8ba0c111-8c37-4aa0-a844-70b2f4ba2f79">

<img width="569" alt="Capture d’écran 2024-07-30 à 15 18 53" src="https://github.com/user-attachments/assets/1e97e214-5b2a-4ac3-9999-8869c9631cb8">
