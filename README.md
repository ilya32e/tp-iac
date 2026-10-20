# TP Jour 3 — Terraform et GitLab CI/CD

## Infrastructure

Le projet provisionne localement avec Docker :

- l'image `nginx:latest` ;
- le réseau `tp3-network` ;
- le conteneur `tp3-web`, accessible sur le port `8081`.

Commandes principales :

```powershell
terraform init
terraform fmt -check
terraform validate
terraform plan
terraform apply
terraform state list
terraform graph
```

Pour vérifier le site : `Invoke-RestMethod http://localhost:8081`.

## Questions de compréhension

1. Le port publié fait partie de la configuration du conteneur Docker. Le provider Docker ne peut pas modifier ce mapping sur place ; Terraform remplace donc le conteneur. Le réseau et l'image n'ont pas changé, ils restent réutilisés.

2. La référence `docker_network.tp3_net.name` dans le bloc `networks_advanced` crée implicitement la dépendance. Il n'est pas nécessaire d'ajouter `depends_on` : Terraform construit automatiquement le graphe à partir des références entre ressources.

3. Le runner GitLab s'exécute dans l'infrastructure GitLab et n'a pas accès au Docker Desktop local. `terraform validate` vérifie la syntaxe, le format et la cohérence du code sans créer de ressources ; `terraform apply` nécessiterait un runner configuré avec l'accès et les identifiants adaptés.

4. `APP_ENV` est définie dans GitLab pour séparer la configuration du code et pouvoir la changer selon l'environnement, sans modifier ni exposer le dépôt. Écrite en clair dans `.gitlab-ci.yml`, elle serait versionnée et visible par toute personne ayant accès au dépôt ; pour une vraie valeur secrète, il faut utiliser une variable CI/CD masquée.
