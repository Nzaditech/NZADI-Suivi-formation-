# Guide Render gratuit — NzadiTech Formation Manager

## Limites importantes du plan gratuit

- Le service Web Render gratuit peut se mettre en veille après une période d'inactivité ; le premier accès après la veille peut être lent.
- La base PostgreSQL gratuite de Render est temporaire et expire après 30 jours. Les données peuvent devenir indisponibles/supprimées à l'expiration : ce mode convient aux essais, pas à une exploitation réelle.
- Avant la fin de la période gratuite, prévois une migration vers une base persistante ou un plan payant et exporte les données. Ne stocke pas de données personnelles réelles sur cette instance de démonstration.
- Si Render refuse de créer la base gratuite via Blueprint sur ton compte, crée le service Web gratuit séparément et utilise une base PostgreSQL externe compatible en renseignant `DATABASE_URL`.

## Déploiement Blueprint

1. Créer un dépôt Git privé sur GitHub et y envoyer le contenu de l'archive.
2. Dans Render : **New + → Blueprint**, connecter le dépôt et appliquer `render.yaml`.
3. Vérifier que Render crée le service Web et la base PostgreSQL gratuits. Si la base gratuite n'est pas proposée dans Blueprint, suis la note ci-dessus.
4. Dans les variables d'environnement du service, relever l'e-mail et le mot de passe générés pour le compte initial. Ne pas les copier dans le code ni dans Git.
5. Attendre le statut `Live` et tester `/api/health`.
6. Se connecter à l'application, créer des fiches fictives de test, vérifier les droits et confirmer que les données restent présentes après un redéploiement.

## Alternative : ressources Render créées manuellement

- Créer une base PostgreSQL Render.
- Créer un Web Service depuis le dépôt Git.
- Build command : `npm install`
- Start command : `npm start`
- Ajouter `DATABASE_URL` (URL interne de la base), `NODE_ENV=production`, `JWT_SECRET` (secret aléatoire de 32 caractères ou plus), `SEED_ADMIN_NAME`, `SEED_ADMIN_EMAIL`, `SEED_ADMIN_PASSWORD` (au moins 10 caractères) et `SEED_CENTER_NAME`.
- Health check path : `/api/health`.

## Dépannage

- `DATABASE_URL manquant` : ajouter l'URL de PostgreSQL aux variables du service.
- `password ...` / erreur de connexion SQL : vérifier la chaîne `DATABASE_URL` et l'état de la base.
- `JWT_SECRET doit contenir...` : définir un secret long, aléatoire et privé.
- `SEED_ADMIN_PASSWORD...` : définir un mot de passe initial d'au moins 10 caractères.
- Login refusé : vérifier l'adresse de `SEED_ADMIN_EMAIL` et le mot de passe affichés dans les variables Render ; un compte déjà créé n'est pas réinitialisé automatiquement au redémarrage.
