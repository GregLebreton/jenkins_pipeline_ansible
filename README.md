 # DEVOPS 2019 # GLB #

        ***
SUJET:
créer un pipeline Jenkins installant un environnement 3 tiers :
  - toolserver --> depot de tools
  - webserver  --> httpd with mod_jk to redirect to appserver
  - appserver  --> httpd, tomcat with app.jar deployed
  
Le pipeline va ensuite récupérer les sources du projet et les playbooks sur un Git, installe l'environnement et config les trois machines (webserver: apache et mod-jk appserver: apache, tomcat), puis par maven build, test et deployement sur repo Nexus avant de le copier pour déployement sur tomcat de appserver.


DONE:
creation d'un pipeline Jenkins qui fait un git checkout, invoque un playbook pour installation et configuration d'un appserver et webserver, test le projet, le build puis le deploy sur le repos Nexus.


TODO:
stage qui récupère le .jar sur Nexus pour le copir sur appserver dans webapps (pour déployement automatique)

        ***

*** branche used: jenkins_ansible_maven_job ***
