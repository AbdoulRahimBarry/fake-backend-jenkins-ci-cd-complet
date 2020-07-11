# Fake-backend-CD en utilisant Ansible && Jenkins

fffffffffffffffffffffffffffffffffffffffffff

Infrastructure: 3 instances VM Centos(ami-0083662ba17882949): Build, Preprod && Prod
1 Serveurs Jenkins

NB: Apres le clone, changer juste le fichier hosts pour mettre les @IP des VMs

****Demarrer la stack jenkins (jenkins-playbook.yml)

via le service Cloud formation de AWS

*Se connecter via un navigateur avec le port 80

*Telecharger les plugins

github integration ---> integration de github

Embeddable Build Status ---> gestion des badges

*Credentials

creer des credentials private-key & vault-key

private-key ---> secret-file

vault-key ---> secret-texte

*Git cloner repo contenant le projet

(fake-backend, battleboat, Jenkinsfile, Playbook.yml) : htps://github.com/abdoulrahi

rm -rf .git/ : (supprimer le lien vers ce repo)

git init : (initialiser un nouveau repo afin qu'il soit "origin")

git remote add origin htps://github.com/abdoulrahimbarry/fake-backend-jenkins-ci-ci.git

*Modifier le fichier hosts

Indiquer les nouvelles adresses VM (build, preprod & prod)

*Administrer jenkins-->configuration du systeme-->GithubServer-->

Avancé(copier l'url proposé en cliquant sur la case à cocher)

*Creer un job fake-backend-jenkinsCD (Pipeline)

Description : Github project(preciser le lien du repo) : htps://github.com/abdoulrahimbar

Build Triggers : GitHub hook trigger for GITScm polling

Pipeline : Pipeline script from SCM -> SCM: Git , Repo: (preciser votre repo)

branch to build: */master , */deve (A preciser Les deux branches )

Script Path: Jenkinsfile

*Sur la branche master pusher le README.md par exemple(mais pas forcement )

Creer une branche deve et Pusher tout le projet sur cette branche

git checkout -b deve

git add .

git commit -m "first update"

git push origin deve

*Ouvrir le port 80 environnement de prod et preprod

(security group sur AWS) car les instances ont uniquement le port 22 ouverts

*Second methode: multipipeline

Pugin: pipeline multibranch ---> deploiement sur plusieurs branches

Les etapes  1 à 8 sont identiques à la premiere methode

creer un job fake-backend-jenkinsCD (Multibranch Pipeline)

Branch Sources --> Git: Project Repository: (Preciser le repo)

Build Configuration --> Mode: By Jenkinsfile, Script Path: Jenkinsfile

Ouvrir le port 80 environnement de prod et preprod

(security group sur AWS) car les instances ont uniquement le port 22 ouverts
