.. _changelog:

.. title:: Changelog

Ghost Changelog
===============

.. toctree::
    :maxdepth: 2


Ghost 16.05.2
-------------

* Global
    - Gestion du multi compte AWS (utilisation du AWS STS Assume Role pour gérer les ressources sur le compte distant) [GHOST-208]

* WebUI
    - Le header et son menu sont maintenant responsives (compatibilité Mobile) [GHOST-254]

* Core/API
    - Possibilité d'utiliser multiples clé SSH dans Ghost pour les déploiements (par région, par compte, par env, par app, etc.) [GHOST-225]

Ghost 16.05.1
-------------

* Core/API
    - Nouveaux environnements disponibles: int, uat, oat [GHOST-247]
    - Ajout de l'IP privé des instances démarrées par Ghost dans le Hotname (et par extension dans le PROMPT PS1) [GHOST-250]
    - Spécification d'un AWS IAM Instance Profile spécifique au lancement de Packer. Permet d'avoir des policy AWS qui pourraient être nécessaire au `buildimage` [GHOST-245]

* Améliorations & Correctifs de bogues
    - Ajout de l'option `ssh_pty` à l'appel Packer (nécessaire sur RedHat/CentOS) [GHOST-246]


Ghost 16.05
-----------

* WebUI
    - Ajout de descriptions sur l'ensemble des champs lors de l'édition d'application [GHOST-236]
    - Better Job Log view (Possibilité de collapse/expand les commandes, coloration, ajout du temps d'exécution de chaque commande) [GHOST-199]
    - Améliorations du footer (meilleure gestion de la version Ghost à afficher) [GHOST-218]
    - Boutton de refresh pour les listes de Subnet et de SecurityGroups [GHOST-167]
    - Possibilité de déployer plusieurs ou tous les modules avec la commande `deploy` [GHOST-240]

* Core/API
    - La commande `updatelifecyclehooks` doit aussi mettre à jour l'AutoScale (LaunchConfig userdata) [GHOST-168]
    - La commande `buildimage` ne clone que la branche SALT nécessaire au provisionning [GHOST-206]
    - Les scripts `stage1` et `stage2` utilise le binaire AWS (cli) depuis le $PATH [GHOST-235]
    - Nouveau role disponible: 'webcache' [GHOST-222]
    - Possibilité d'utiliser la nouvelle option `Safe Deployment` avec la commande deploy [GHOST-142]
      Plus d'informations sur la documentation: https://demo.ghost.morea.fr/doc/rst/commands.html#run-deploy

* Améliorations & Correctifs de bogues
    - Packer provisionne curl uniquement si il faut installer SALT (Skip Salt Bootstrap option) [GHOST-234]
    - Possibilité d'utiliser `ec2-user` à la place d'`admin` [GHOST-231]
    - Meilleure gestion des erreurs d'API AWS dans la WebUI [GHOST-233]
    - Ajout des nouveaux types de Volume EBS AWS [GHOST-238]
    - Meilleure gestion des erreurs sur le nettoyage des scripts au stage2 (pre-deploy, post-deploy, buildpack) [GHOST-232]
    - Suppression des fichiers temporaires sur Ghost (Manifest tempon) [GHOST-230]
    - Plus besoin de chown dans le script stage2 les dossiers des modules avant déploiements (les modules ont pour UID et GID les valeurs spécifiées dans l'app) [GHOST-237]

Ghost 16.04
-----------

* WebUI
    - Ajout des types d'instances EC2 sur la région Chine (cn-north-1) [GHOST-219]
    - Désactivation de l'auto-scroll sur la vue log d'un job quand l'utilisateur utilise sa molette [GHOST-223]
    - Refonte du header et ajout d'un footer avec la version courante de Ghost [GHOST-218]
    - Ajout des descriptions des commandes [GHOST-217]

* Core/API
    - Le nombre de LaunchConfig à conserver sur l'AutoScaling pour pouvoir Rollback est maintenant configurable [GHOST-195]
    - Configuration automatique du Hostname des instances démarrées par l'AutoScaling [GHOST-226]
    - Mise à jour des dépendances Python (requirements.txt) [GHOST-220]
    - A la suppression d'un module, nettoyage des dossiers locaux liés au module supprimé [GHOST-177]
    - Possibilité de choisir si Packer doit installer Salt avant de provisionner l'AMI [GHOST-171]

* Améliorations & Correctifs de bogues
    - Correctifs sur le script de sauvegarde Ghost, permet l'automatisation de sa mise en place [GHOST-224]
    - Déplacement de la valeur PAGINATION_DEFAULT de settings.py vers config.yml [GHOST-175]

Ghost 16.03
-----------

* WebUI
    - Possibilité de ré-ordonner les modules d'une application Ghost via drag'n drop sur le menu de gauche [GHOST-113]
    - Commande "deploy" par défaut [GHOST-205]
    - Nouveau style pour les boutons d'actions sur les listes [GHOST-207]
    - Bouton pour rafraîchir les Select (peuplés depuis AWS) sur l'édition d'application [GHOST-167]
    - Coloration syntaxique shell/bash pour les Textarea, avec numérotation de ligne et police à taille fixe  (pre-deploy, post-deploy, buildpack) [GHOST-215]

* Core/API
    - Création du dossier de destination lors du déploiement d'un module si celui-ci n'existe pas (script stage2) [GHOST-212]
    - Lors d'un Deploy/Re-Deploy, le manifest est re-ordonné suivant l'ordre des modules définis dans l'application Ghost [GHOST-113]
    - Nouvelles variables d'environnement disponibles pour les scripts de pre-deploy & post-deploy [GHOST-210]. Pour rappel, voici la liste des variables disponibles :
         * GHOST_APP
         * GHOST_ENV
         * GHOST_ROLE
         * GHOST_MODULE_NAME
         * GHOST_MODULE_PATH
         * GHOST_MODULE_USER
         * GHOST_MODULE_REPO
         * GHOST_MODULE_REV
         * GHOST_MODULE_COMMIT
         * GHOST_MODULE_COMMIT_MESSAGE
    - Nouvelle commande "Update auto scaling group" disponible [GHOST-48]

* Améliorations & Correctifs de bogues
    - Amélioration du nettoyage des anciennes révisions de modules sur les instances (libération d'espace disque) [GHOST-211]
    - Utilisation de noms explicites pour les fichiers de logs Packer [GHOST-214]
    - Refactoring de la commande Create Instance [GHOST-169]

Ghost 16.02
-----------

* WebUI
    - Vue sur les Ressources AWS d'une application (AS, ELB, Instances EC2) [GHOST-102]
    - Thème Material Design (guidelines Google) [GHOST-143]
    - Auto-complétion sur les listes [GHOST-170]
    - Button pour mettre la console de log (vue Job) en mode théâtre [GHOST-188]
    - Protection du double clic sur les boutons de validation (évite de lancer 2 jobs) [GHOST-180]
    - Récupération des KeyPairs & Instances Profiles depuis API AWS [GHOST-178]

* Core/API
    - 3 Stratégies de Worker possibles pour une instance Ghost : 1 par app, 1 par env, 1 pour l'instance [GHOST-193]
    - Possibilité de définir les UID & GID des fichiers déployés par un module [GHOST-187]
    - Renommage de la commande "Rollback" en "Redeploy" [GHOST-173]
    - Renommage de la commande "Destroy instance" en "Destroy all instances" [GHOST-186]
    - Stratégies de déploiements : Séquentiel ou parallèle sur les instances (config + option de deploy) [GHOST-82]
    - Suppression des scripts de Predeploy & Postdeploy après exécution [GHOST-189]
    - Suppression du script de Buildpack après exécution [GHOST-190]
    - Déploiement cross-region AWS [GHOST-158]
    - Dépôt SALT configurable [GHOST-157]

* Améliorations & Correctifs de bogues
    - Optimisations sur la récupération des derniers déploiements réussis pour chaque module d'une application [GHOST-172]
    - Refactoring de code [GHOST-163/164/181]
    - Commandes découvertes à la volée [GHOST-30]
    - Attente de la disponibilité des tags sur les instances EC2 avant de continuer les déploiements [GHOST-185]


Ghost 16.01
-----------

* WebUI [GHOST-150, GHOST-155, GHOST-152, GHOST-160, GHOST-138, GHOST-139, GHOST-128, GHOST-55, GHOST-174]
    - Correctif sur la fonction Cloner une Application : rafraichissement des selects
    - Changement des couleurs de fonds sur les listes (retrait du rouge et du vert trop vif remonté par les utilisateurs)
    - Vue liste d'application : recherche et filtres
    - Vue liste des jobs : recherche et filtres
    - La vue Job (détail) se rafraichit automatiquement lors d'un changement d'état
    - Une popover de warning sur le champs Module Path lors de l'édition d'une application si le champ contient une mauvaise valeur : /, /tmp, /etc, /var
    - Défilement infini sur les pages de listes (récupération des données en asynchrones)
    - Logo Ghost & Favicon
    - Fix et correctifs CSS

* Core/API
    - Possibilité d'avoir un dépôt Git spécifique pour les formulas SALT d'une instance Ghost [GHOST-156]
    - Nouvelle commande updatelifecyclehooks : permet d'avoir des scripts de pre_bootstrap et post_bootstrap [GHOST-159]
    - MAX_DEPLOY_HISTORY devient configurable (nombre de révisions de déploiement à conserver) [GHOST-147]
    - Autorisation du caractère "+" dans le champ version des Features [GHOST-145]
    - La variable TMPDIR est définie pour Packer : permet d'avoir les fichiers de logs et temporaires de Packer dans /var/log/ghost/packer [GHOST-166]
    - Nouvelle de stratégie de git clone/pull/mirror sur l'instance Ghost : permet des déploiements beaucoup plus rapides [GHOST-104]

* Script
    - Ghost Backup : possibilité de passer en argument la région S3 de backup (ou spécifiée dans la config de Ghost) [GHOST-146]

* Correctifs de bogues
    - Meilleure prise en compte du code de retour du script pre-deploy [GHOST-151]
    - Meilleur affichage des modules dans les mails de notifications [GHOST-148]
    - Correctif sur le status Auto-scaling (ne doit pas rester en Suspended quand un déploiement échoue) [GHOST-136]

Ghost 15.12
-----------

* Nouvelle interface graphique du client Web [GHOST-44, GHOST-45, GHOST-79, GHOST-93, GHOST-94, GHOST-109, GHOST-115, GHOST-119, GHOST-132, GHOST-134, GHOST-135, GHOST-137]
    - Couleurs pour identifier les environnements _>>> À noter, nous avons déjà eu plusieurs retours négatifs concernant le code couleur utilisé pour distinguer les environnements. Nous allons rectifier le tir dans la version 15.12
    - Picto sur les boutons d’actions (identification plus rapide)
    - Menu flottant sur les vues d’application
    - Header flottant pour mieux voir quel objet est en cours de traitement
    - Plusieurs champs texte remplacés par des Selects pour une saisie plus rapide
    - Revue des valeurs par défaut des champs
    - Amélioration sur la vue « console » (log d’un job)
    - Ajout de RegExp sur le modèle, permet d’éviter des erreurs de caractères non supportés
    - Lien d’accès au dernier déploiement réussi dans la vue Application, tableau de module

* Déploiement parallèle [GHOST-89, GHOST-121]
    - Chaque application possède sa file d’attente de Job
    - Chaque application possède son Worker pour dépiler sa file

* Nettoyage de vieux reliquats [GHOST-36]

* Variable de contexte pour les scripts de Buildpack, Pre-Deploy, Post-Deploy [GHOST-61]

* Possibilité d’annuler un Job qui est en attente (ne peut pas être annulé si déjà démarré) [GHOST-87]

* Meilleure gestion des états d’instances lié aux Auto-Scaling Groups [GHOST-110, GHOST-117]

* Possibilité de choisir le type d’instance EC2 lors du buildimage (peut être différent du type d’instance par défaut de l’application) [GHOST-130]

* Bug fixes [GHOST-108, GHOST-127, GHOST-129, GHOST-131, GHOST-140]

