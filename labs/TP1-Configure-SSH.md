# Configurer SSH entre les conteneurs



## Configurer l'environement


Générer les clés SSH sur le serveur Ansible
```
ssh-keygen -t rsa -b 2048

```
Copier la clé publique vers les nodes cibles
```
ssh-copy-id ansible_user@<node1>
ssh-copy-id ansible_user@<node2>
```
Tester la connexion SSH
```
ssh ansible_user@<node1>
exit
ssh ansible_user@<node2>
exit
```

## Utiliser Ansible pour tester la configuration


Créez un fichier inventory pour référencer vos nodes :

```
[node] 
ansible_node1 ansible_host=<node1> ansible_user=ansible_user ansible_become_password=password
ansible_node2 ansible_host=<node2> ansible_user=ansible_user ansible_become_password=password

```
Ensuite, testez Ansible via une commande ad hoc :
```
ansible -i inventory node -m ping
```
## Configurer les privilèges sudo sans mot de passe
Vous pouvez modifier la configuration sudo sur les nœuds cibles pour permettre à Ansible de devenir super-utilisateur sans demander de mot de passe.

- Connectez-vous sur chaque node cible avec ssh.

- Ajoutez la configuration suivante au fichier /etc/sudoers :
```
echo "ansible_user ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
```
Cela permet à app_user d'utiliser sudo sans fournir de mot de passe.
