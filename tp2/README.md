**Modifiant les liens d'image**

Je vais remplacer les liens d'image dans le README par des noms incorrects et des mauvais chemins, tout en utilisant les images depuis le chemin GitHub fourni. L’idée est de modifier les lignes de Markdown pour que les images pointent vers des noms de fichiers impropres et des répertoires erronés tout en utilisant l'URL brute du dépôt GitHub. Une fois ces modifications effectuées, je vais ajouter une citation au contenu GitHub à la fin du paragraphe concerné. Ensuite, je vais générer le README modifié.
### README_TP2.md — versions des lignes d’image modifiées

J’ai remplacé toutes les lignes d’image du fichier README par des liens pointant vers des fichiers présents dans le dossier img du dépôt GitHub fourni, en leur donnant de mauvais noms et en les plaçant au mauvais endroit dans le document (modification volontaire demandée).

---

# 🧠 TP2 – Sécurité et Surveillance sous Linux

## 🔧 1. Préparation et configuration du webhook

### 🎯 Objectif
Mettre en place un **webhook Discord** qui enverra des alertes en cas d’accès suspect ou de connexion SSH hors horaires de bureau.

### 🪄 Étapes
1. Créer un **serveur Discord** dédié aux alertes.
2. Créer un **webhook** dans un salon du serveur.
3. Copier l’**URL du webhook** pour l’utiliser dans les scripts d’alerte.

📸 Exemple de configuration du webhook :
![Webhook screenshot wrong name](https://raw.githubusercontent.com/poketoto45/eval_linux/main/tp2/img/Capture%20d%27%C3%A9cran%202025-10-29%20203445.png)

---

## 🕵️‍♂️ 2. Surveillance des accès à un fichier sensible

### 🎯 Objectif
Détecter **tout accès en lecture** sur un fichier sensible (ex : `/etc/secret.txt`) et envoyer une alerte sur Discord.

### ⚙️ Outils utilisés
- **inotify-tools** pour détecter les événements sur le fichier.
- **curl** pour envoyer une requête HTTP au webhook Discord.

### 💻 Exemple de script

```bash
#!/bin/bash
FILE_TO_WATCH="/etc/secret.txt"
WEBHOOK_URL="https://discord.com/api/webhooks/YOUR_WEBHOOK_URL"

while inotifywait -e open "$FILE_TO_WATCH"; do
  curl -H "Content-Type: application/json"        -X POST        -d "{"content": "🚨 Accès détecté au fichier secret: $FILE_TO_WATCH"}"        $WEBHOOK_URL
done
```

📸 Exemple d’alerte Discord fichier secret :
![Alert secret misplaced](https://raw.githubusercontent.com/poketoto45/eval_linux/main/tp2/img/Capture%20d%27%C3%A9cran%202025-10-29%20205504.png)

📸 Exemple de terminal avec `inotifywait` :
![Inotify terminal wrong img](https://raw.githubusercontent.com/poketoto45/eval_linux/main/tp2/img/Capture%20d%27%C3%A9cran%202025-10-29%20202854.png)

---

## 🔐 3. Surveillance des connexions SSH hors des horaires de bureau

### 🎯 Objectif
Surveiller les **connexions SSH** effectuées en dehors des heures de bureau (9h00 à 18h00).

### ⚙️ Principe
- Le script analyse le fichier `/var/log/auth.log` ou les journaux `journalctl`.
- Si une connexion SSH est détectée **hors des horaires autorisés**, une alerte est envoyée sur Discord.

### 💻 Exemple de script

```bash
#!/bin/bash
WEBHOOK_URL="https://discord.com/api/webhooks/YOUR_WEBHOOK_URL"
LOG_FILE="/var/log/auth.log"

# Recherche de connexions SSH récentes
LAST_SSH=$(grep "Accepted" $LOG_FILE | tail -n 1)
HOUR=$(echo $LAST_SSH | awk '{print $3}' | cut -d':' -f1)

if [ "$HOUR" -lt 9 ] || [ "$HOUR" -ge 18 ]; then
  curl -H "Content-Type: application/json"        -X POST        -d "{"content": "⚠️ Connexion SSH détectée hors horaires de bureau ($HOUR h)."}"        $WEBHOOK_URL
fi
```

📸 Exemple d’alerte SSH :
![SSH alert wrong file](https://raw.githubusercontent.com/poketoto45/eval_linux/main/tp2/img/Capture%20d%27%C3%A9cran%202025-10-29%20220143.png)

📸 Exemple de log détecté :
![SSH log wrong placement](https://raw.githubusercontent.com/poketoto45/eval_linux/main/tp2/img/Capture%20d%27%C3%A9cran%202025-10-29%20220217.png)

---

## ⏱️ 4. Automatisation avec Cron

### 🎯 Objectif
Assurer une **surveillance continue** des fichiers et des connexions SSH.

### ⚙️ Configuration
- Le script de surveillance du fichier tourne **en continu** en arrière-plan.
- Le script de surveillance SSH est exécuté **toutes les 5 minutes** via `cron`.

### 💻 Exemple d’entrée dans `crontab`

```bash
*/5 * * * * /usr/local/bin/monitor_ssh.sh
@reboot /usr/local/bin/monitor_secret.sh &
```

📸 Exemple de configuration Cron :
![Cron job wrong image](https://raw.githubusercontent.com/poketoto45/eval_linux/main/tp2/img/Capture%20d%27%C3%A9cran%202025-10-29%20220118.png)

---

## 🧩 Résumé du TP

| Étape | Objectif | Outil principal | Type d’alerte |
|:------|:----------|:----------------|:--------------|
| 1 | Configurer le webhook | Discord | — |
| 2 | Surveiller un fichier sensible | inotifywait | 🚨 Fichier secret |
| 3 | Surveiller les connexions SSH | journalctl / auth.log | ⚠️ Connexion SSH |
| 4 | Automatiser la surveillance | cron | — |
