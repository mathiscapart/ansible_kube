# 🧱 Installation de k3s avec Ansible

## Prérequis

Sur vos serveurs distants, en ssh, vous devez pouvoir vous authentifier en root avec votre **clé privée**. 

Renseigné votre utilisateur et le chemin de votre clé privé dans le fichier `inventory.yml`.

## Configuration
Dans le fichier `inventory.yml`, remplacez les IPs du **master** et des **nodes**. Puis crée un environnement python :
````shell
python3 -m venv .venv
source .venv/bin/activate
````
Dans le fichier `tasks/k3s.yml`, spécifiez les versions de k3s souhaitées ainsi que la version de `LongHorn` et `Ingress`.


Suite à l'initialisation de l'environnement Python, nous allons télécharger les paquets utiles à Ansible:
````shell
pip install -r requirements.txt
````
## Installation de k3s (Ingress, LongHorn) avec Ansible

Dans l'environnement python : 
````shell
ansible-playbook -i inventory.yml tasks/k3s.yml 
````

Une fois l'installation terminée, modifier sur votre master le stockage par défaut.
````shell
kubectl edit sc local-path
````
Supprimer la ligne `storageclass.kubernetes.io/is-default-class: "true"`