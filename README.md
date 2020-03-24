# Quelques librairie en Data Science en Python

## Objectifs pédagogiques

*   Modifier et exécuter un notebook Jupyter
*   Créer et installer des modules Python
*   Visualiser des données avec Matplotlib et Seaborn
*   Manipuler des tableaux avec Numpy
*   Manipuler un jeu de données grâce à Pandas

## Installation de Anaconda sur mon VPS
* d'abord il faut aller sur le site officielle de anaconda récupérer 
   le lien suivant: <a href="https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh">https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh</a>
* et puis on télécharge anaconda dans son serveur avec la commande suivante:
	<code>wget https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh</code>
	et ensuite on peut faire un <code>ls</code> pour voir si le fichier est bien telecharger
* si tout se passe bien, on tappe encore la commande la <code>which pip</code> on devrait voir
	<code>~/anaconda3/bin/pip</code> et à partir de là anaconda est install dans le
	serveur


## Configurez Jupyter pour les accès distants
* 	tout d'abord il faut générer un fichier de configuration la commande 
	suivante <code>jupyter notebook --generate-config</code>
*   vous allons générer un mot de passe qui permettra aux users
	de se logger avec pour travailler à distance avec la commande suivante:
	<code>key=$(python -c "from notebook.auth import passwd; print(passwd())")</code>
	l'invite de commande nous invitera à saisir notre mot de passe et sa configuration

## Configurez le protocole HTTPS pour Jupyter avec un certificat self-signed
pour cela, il faut tapper la commande suivante:
<code>
<pre>
	cd ~
	mkdir certs
	cd certs
	certdir=$(pwd)
	openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.key -out mycert.pem
</pre>
</code>
ensuite <code>Entrée</code> jusqu'à ce que le certificat soit générer si vous voulez vous pouvez 
donnez vos renseignements perso.

## Modifiez le fichier de configuration de Jupyter
	pour cela, il faut renseigner les information de notre certificat qu'on vient de générer avec 
	la commande suivante.
<code>
<pre>
	cd ~
	sed -i "1a\
	c = get_config()\\
	c.NotebookApp.certfile = u\'$certdir/mycert.pem\'\\
	c.NotebookApp.keyfile = u\'$certdir/mycert.key\'\\
	c.NotebookApp.ip = '*'\\
	c.NotebookApp.open_browser = False\\
	c.NotebookApp.password = u\'$key\'\\
	c.NotebookApp.port = 8888" .jupyter/jupyter_notebook_config.py
</pre>
</code> 
*  et à partir de là, on est près on peut lancer le serveur maintenant avec cette commande:
   <code>jupyter notebook --allow-root</code> et puis comme vous pouvez le voir dans la commande précédente 
*  le port **8888** il vous suffit tappez l'adresse **IP** ou **nom de domaine** lié à votre serveur
   pour avoir accèss à votre **jupyter notebook** pour vos analyse de donnez

## Premiers Pas avec Python
*   Pour commencer, on crée un fichier avec extension ipnb
    ensuite on tape note commande pyhon
*   pour créer un fichier disponible dans tous nos scripts, il faut créer un fichier d'extension **.py**
	et puis créer nos **fonctions ou class** ensuite les importées et les utilisées 
