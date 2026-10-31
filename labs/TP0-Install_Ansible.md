# Installation des machines Ansible



## builder et configurer l'environnement avec docker


```
cd existing_repo
```
utiliser docker compose pour monter un serveur ansible et deux nodes cibles
```
docker compose up -d --build

 Récupérer les adresses IP des conteneurs (node1 et node2)
```
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ansible_node1 
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ansible_node2
```
Générer les clés SSH sur le serveur Ansible
```
docker exec -it ansible_server bash
su - ansible_user 
```