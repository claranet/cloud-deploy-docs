.. _changelog:

.. title:: Changelog

Ghost Changelog
===============

.. toctree::
    :maxdepth: 2

Ghost 17.01
-----------

* WebUI
    - Ghost instance health status (footer button) [GHOST-204]
    - Orange warning color when choosing a big instance type [GHOST-338]
    - Adding z-index for footer, updating left bar height dynamically [GHOST-325]
    - Setting infinite scrolling limit to work with size rounding in zoomed in or out window (float sizes) [GHPST-302]
    - Setting static path for command page JS get last revision route [GHOST-332]

* Core/API
    - Do not install curl before bootstrapping SaltStack (requires Packer v0.12.1+) [GHOST-334]
    - Option "Destroy temporary ELB" for ``purgebluegreen`` command [GHOST-303]
    - Verify deployed module name too when using ``preparebluegreen`` [GHOST-287]

* Improvements & Bug fixes
    - Ensure Ghost tags are properly set (on AutoScale and standalone instances) [GHOST-336]

Ghost 16.12
-----------

* WebUI
    - Handle ALB/TargetGroups in UI (app infos) [GHOST-310]

* Core/API
    - Handle Application Load Balancer in SafeDeployment [GHOST-310]
    - Correct ASG boto2 errors when ALB is used by upgrading to boto3 [GHOST-309]
    - Keep a local mirror of morea-salt-formulas & zabbix GIT repos [GHOST-271]
    - Allow creating Launch Configurations with Detailed EC2 Instance Monitoring enabled, on a per app basis [GHOST-162]
    - Move to EVE swagger for API documentation [GHOST-329]

* Improvements & Bug fixes
    - Hotfix "Run more like this (caused by GHOST-291) [GHOST-330]
    - Docker-compose: add nginx container for better local tests [GHOST-331]
    - Upgrade to boto v2.45.0: handle new AWS regions (eu-west-2,ca-central-1,us-east-2,ap-south-1) [GHOST-339]
    - Colorized error messages in stage2 [GHOST-340]
    - Create empty MANIFEST if nonexistent upon successful buildimage to allow instance bootstrapping [GHOST-341]
    - Ensure Ghost tags are properly set when using ``updateautoscaling``, ``createinstance`` and ``preparebluegreen`` commands [GHOST-336]

Ghost 16.10
-----------

* WebUI
    - Handle ``createinstance`` job in ``Run more like this`` action [GHOST-291]
    - Using / to check auth rather than /apps which could hurt performance [GHOST-322]
    - Move get_envs call to specific template that need it [GHOST-322]
    - Use tabs per env for app list [GHOST-307]
    - Init provider JS param when cross account activated [GHOST-295]
    - Replace Morea references in the webUI and in the config file by Claranet [GHOST-308]

* Core/API
    - Passing mongo and Redis config in Command class [GHOST-318]
    - Add ssh config to backup [GHOST-314]

* Improvements & Bug fixes
    - Command ``swapbluegreen`` should stop when the offline ELB is not correctly configured [GHOST-292]
    - Add suspend and resume AutoScaling process in ``preparebluegreen`` command [GHOST-327]
    - Docker-compose update to version 2 [GHOST-320]
    - Adding jetbrains clauses to gitignore [GHOST-315]

Ghost 16.09.1
-------------

* Improvements & Bug fixes
    - Update boto3, botocore and awscli pip dependencies [GHOST-311]
    - Fix ``prepare`` command option [GHOST-229]
    - Hotfix - use custom app tags only if setted [GHOST-243]
    - Fix ASG listing when ALB are assotiated by using boto3 [GHOST-309]

Ghost 16.09
-----------

* WebUI
    - CodeMirror scripts upgrade - better script area in UI [GHOST-215]
    - Show Optional volumes in ``app_view`` [GHOST-306]
    - Replace Packer output placeholders in logs by HTML one [GHOST-298]
    - Hotfix [GHOST-229] Don't show ``blue`` bubble when BG is not enabled

* Core/API
    - Allow custom EC2 Tags per application, auto applying Ghost specific Tags [GHOST-243/GHOST-244]
    - Handle per application custom environment variables. Thoses variables will be available in many scripts from the ``deploy`` and ``build`` workflow. (more details here: :ref:`scripts_vars`) [GHOST-216]
    - Rollback application manifest if a ``deploy`` or ``redeploy`` command fails [GHOST-286]
    - Feature preset import, permits to bulk import some features in an application based on ready-to-use preset [GHOST-133]
    - Add seconds when generating LaunchConfig name to avoid naming collisions [GHOST-301]
    - Docker compose file and and Redis/Mongo endpoints configurable [GHOST-153]

* Improvements & Bug fixes
    - An AutoScale Group is now mandatory to use Safe Deploy [GHOST-280]
    - Stage2 script now follows symlinks when updating Zabbix config [GHOST-285]
    - Version field in feature can be empty/null [GHOST-270]
    - AWS EC2 instance type updated
    - Python modules upgraded (boto*)

Ghost 16.07.1
-------------

* Improvements & Bug fixes
    - Hotfix [GHOST-229]: fix redeploy command broken by refactoring
    - Hotfix [GHOST-229]: boto3 addition upgrades botocore which breaks awscli 1.4 (from wheezy) so also update awscli

Ghost 16.07
-----------

* WebUI
    - Add ``Documentation`` link in footer [GHOST-183]
    - WTForm SelectField override to handle no available selected data [GHOST-278]
    - Show S3 link to module package in Deployment view [GHOST-277]
    - Also display AMIs from specific third party AWS accounts [GHOST-276]
    - [UI] Drag'n'drop Features order [GHOST-274]

* Core/API
    - Blue/Green deployment strategy [GHOST-229] (more info here: :ref:`bluegreen`)
    - Add ami-base role for base AMI building [GHOST-275]
    - Role field now generic (a specific role can be created) [GHOST-241]

* Improvements & Bug fixes
    - Clean Error for empty boostrap during stage2 execution [GHOST-249]
    - Refactor ``destroyallinstances`` command [GHOST-273]
    - Hotfix [GHOST-102] show Ghost tag instances bug

Ghost 16.06
-----------

* WebUI
    - [UI] Quick access boutons on "Completed view" [GHOST-252]
    - JS Fix for CrossAccount credential check [GHOST-267]

* Core/API
    - Add generated hostname to /etc/hosts for private IP resolution [GHOST-251]
    - Add private IP option and Subnet option in ``createinstance`` command [GHOST-248]
    - AMI retention purge is now configurable [GHOST-259]
    - Handle fabric errors, Job will be marked as failed if one ``predeloy`` or ``postdeploy`` script fails [GHOST-265]
    - ghost-doc repo as Submodule [GHOST-183]
    - Add the 'After all deploy' script available, triggered on Ghost after the deployment on every instances [GHOST-255]
    - Pre and Post Buildimage hooks, custom scripts to tweak AMI if needed [GHOST-253]
    - Features with multiple pillar parameter values, allow us to be more flexible on SALT formulas [GHOST-270]
    - Handle UTF-8 characters in base64 encoded scripts (pre-bootstrap, post-bootstrap, buildpack, pre-deploy, post-deploy, after-all-deploy, pre-buildimage, post-buildimage) [GHOST-264]

* Improvements & Bug fixes
    - Fix safe deployment with cross account and spaces issue [GHOST-142]
    - getconf HOST_NAME_MAX to truncate hostname [GHOST-263]
    - Allow installation of arbitrary gems [GHOST-258]
    - Hotfix to handle buttons when creating/cloning an app [GHOST-252]
    - Update subnets in ``updateautoscale`` command [GHOST-260]
    - use boto.s3.connection.OrdinaryCallingFormat() calling format to support bucket with dots in their name [GHOST-256]

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
    - Spécification d'un AWS IAM Instance Profile spécifique au lancement de Packer. Permet d'avoir des policy AWS qui pourraient être nécessaire au ``buildimage`` [GHOST-245]

* Améliorations & Correctifs de bogues
    - Ajout de l'option ``ssh_pty`` à l'appel Packer (nécessaire sur RedHat/CentOS) [GHOST-246]


Ghost 16.05
-----------

* WebUI
    - Ajout de descriptions sur l'ensemble des champs lors de l'édition d'application [GHOST-236]
    - Better Job Log view (Possibilité de collapse/expand les commandes, coloration, ajout du temps d'exécution de chaque commande) [GHOST-199]
    - Améliorations du footer (meilleure gestion de la version Ghost à afficher) [GHOST-218]
    - Boutton de refresh pour les listes de Subnet et de SecurityGroups [GHOST-167]
    - Possibilité de déployer plusieurs ou tous les modules avec la commande ``deploy`` [GHOST-240]

* Core/API
    - La commande ``updatelifecyclehooks`` doit aussi mettre à jour l'AutoScale (LaunchConfig userdata) [GHOST-168]
    - La commande ``buildimage`` ne clone que la branche SALT nécessaire au provisionning [GHOST-206]
    - Les scripts ``stage1`` et ``stage2`` utilise le binaire AWS (cli) depuis le $PATH [GHOST-235]
    - Nouveau role disponible: 'webcache' [GHOST-222]
    - Possibilité d'utiliser la nouvelle option ``Safe Deployment`` avec la commande deploy [GHOST-142]
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

