
# TP 1

## Objectif

Ce TP a pour but d'installer et configurer un serveur web Apache, de sécuriser l'accès avec le pare-feu UFW, et de durcir les connexions SSH. Le README ci-dessous suit les consignes et inclut le code HTML à déployer comme page d'accueil.

---

## 1. Installation et configuration d’un serveur web

1. Installer Apache, lancer le service et vérifier son statut.

   Commandes (exemples pour une distribution Debian/Ubuntu) :

```bash
sudo apt update
sudo apt install -y apache2
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2
```

2. Configurer le serveur pour servir une page web simple.

   Remplacez le contenu de `/var/www/html/index.html` par le code suivant :

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Linux is Better</title>
	<style>
		body {
			background-color: #f0f0f0;
			margin: 0;
			height: 100vh;
			display: flex;
			justify-content: center;
			align-items: center;
			font-family: Arial, sans-serif;
		}
		h1 {
			color: #333;
			font-size: 48px;
			text-align: center;
			animation: fadeIn 2s ease-in-out;
		}
		@keyframes fadeIn {
			from { opacity: 0; }
			to { opacity: 1; }
		}
	</style>
</head>
<body>
	<h1>Linux is better</h1>
</body>
</html>
```

3. Vérifier que le serveur est accessible via un navigateur : ouvrez `http://localhost/` sur la machine local.
ouvrez `http://192.168.1.2` sur la machine externe.

4. Modifier la configuration pour que le serveur réponde sur un port non standard (ex: 8080).

   - Éditez `/etc/apache2/ports.conf` et ajoutez/modifiez la ligne :

```text
Listen 8080
```

   - Éditez ensuite le fichier du site par défaut, généralement `/etc/apache2/sites-available/000-default.conf`, et changez la directive `<VirtualHost *:80>` en `<VirtualHost *:8080>` (ou ajoutez un nouveau VirtualHost sur le port 8080).

   - Redémarrez Apache :

```bash
sudo systemctl restart apache2
```

   - Vérifiez l'accès local via `http://localhost:8080/`.
   - Vérifier l'accès externe via `http://192.168.1.2:8080`.

---

## 2. Configuration du pare-feu avec UFW

1. Autoriser les connexions sur le port du serveur web (ici 8080) et SSH (22), puis activer UFW :

```bash
sudo ufw allow 8080/tcp
sudo ufw allow 22/tcp
sudo ufw enable
sudo ufw status verbose
```

2. Bloquer toutes les autres connexions entrantes : UFW par défaut refuse les connexions entrantes non autorisées après activation si vous n'avez que des règles d'autorisation explicites (cf. commande `sudo ufw default deny incoming`).

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

3. Tester les règles : essayez de vous connecter depuis une autre machine sur un port différent (par ex. 80 ou 3306) pour vérifier que la connexion est refusée.

---

## 3. Sécurisation des connexions SSH

1. Configurer la machine pour accepter uniquement les connexions par clés SSH :

   - Copiez votre clé publique dans `~/.ssh/authorized_keys` pour l'utilisateur voulu.
   - Dans `/etc/ssh/sshd_config` :

```text
# Désactiver l'authentification par mot de passe
PasswordAuthentication no
# Autoriser uniquement l'authentification par clé
PubkeyAuthentication yes
```

2. Désactiver le login root via SSH :

```text
PermitRootLogin no
```

3. Après modification, redémarrez le service SSH :

```bash
sudo systemctl restart sshd
```

4. Important : Avant de désactiver l'authentification par mot de passe, vérifiez que votre clé fonctionne et que vous pouvez vous reconnecter (évite de vous verrouiller hors de la VM).

---

## Vérifications et points d'attention

- Assurez-vous que le port choisi (ex : 8080) est bien ouvert dans UFW.
- Si le serveur est accessible depuis l'extérieur, pensez aux règles supplémentaires (rate-limiting, fail2ban, certificats TLS, etc.).
- Sauvegardez les fichiers de configuration avant modification (ex. `sudo cp /etc/apache2/ports.conf /etc/apache2/ports.conf.bak`).

---

## Images / Captures d'écran
- ![Capture d'écran 163919](image/Capture%20d%27%C3%A9cran%202025-10-26%20163919.png)
- ![Capture d'écran 163948](image/Capture%20d%27%C3%A9cran%202025-10-26%20163948.png)
- ![Capture d'écran 164150](image/Capture%20d%27%C3%A9cran%202025-10-26%20164150.png)
- ![Capture d'écran 164155](image/Capture%20d%27%C3%A9cran%202025-10-26%20164155.png)
- ![Capture d'écran 164159](image/Capture%20d%27%C3%A9cran%202025-10-26%20164159.png)
- ![Capture d'écran 164242](image/Capture%20d%27%C3%A9cran%202025-10-26%20164242.png)
- ![Capture d'écran 164246](image/Capture%20d%27%C3%A9cran%202025-10-26%20164246.png)
- ![Capture d'écran 175944](image/Capture%20d%27%C3%A9cran%202025-10-26%20175944.png)
- ![Capture d'écran 180419](image/Capture%20d%27%C3%A9cran%202025-10-26%20180419.png)
- ![Capture d'écran 180623](image/Capture%20d%27%C3%A9cran%202025-10-26%20180623.png)
- ![Capture d'écran 180630](image/Capture%20d%27%C3%A9cran%202025-10-26%20180630.png)
- ![Capture d'écran 192300](image/Capture%20d%27%C3%A9cran%202025-10-26%20192300.png)
- ![Capture d'écran 193451](image/Capture%20d%27%C3%A9cran%202025-10-26%20193451.png)
- ![Capture d'écran 193653](image/Capture%20d%27%C3%A9cran%202025-10-26%20193653.png)

Si une image ne s'affiche pas correctement, indique-moi son nom exact et je corrigerai le lien ou je renommerai les fichiers pour enlever espaces/accents si tu préfères.
