<<<<<<< HEAD
# NzadiTech Formation Manager — V1 MVP

Application web interne de gestion de centre de formation, inspirée du cahier des charges V2.0. Interface en français, responsive, backend Node.js/Express, PostgreSQL, authentification par jeton et contrôle des accès par rôle.

## Fonctionnalités livrées dans ce MVP

- Connexion du personnel, mot de passe haché avec bcrypt, expiration de session, limitation des tentatives de connexion.
- Rôles : super-administrateur, directeur, secrétaire, responsable pédagogique, comptable et chargé de communication.
- Isolation des enregistrements par centre au niveau des requêtes API.
- Dossiers apprenants et formateurs ; catalogue de formations ; sessions ; inscriptions ; présence ; paiements ; journal de communications.
- Tableau de bord, recherche, exports CSV, reçu imprimable depuis un paiement, rapport financier mensuel.
- Journalisation des opérations d'écriture, API JSON, contrôle de santé `/api/health`.
- Déploiement Render décrit dans `render.yaml`.

## Limites à connaître

Cette livraison est un MVP utilisable pour valider les flux de gestion, pas encore une mise en production financière complète. Les SMS et e-mails ne sont **pas envoyés réellement** : le module communications journalise les messages et signale la nécessité d'un adaptateur fournisseur officiel. La file de tâches, campagnes planifiées, webhooks fournisseurs, évaluations et notes, documents PDF certifiés avec QR, MFA, import Excel, sauvegardes/restauration automatisées, facturation SaaS et interface de super-administration multi-centres avancée restent à développer dans les phases suivantes. Le bouton « Reçu » ouvre une page imprimable pour enregistrer en PDF via le navigateur ; ce n'est pas encore un PDF signé/certifié.

## Déployer sur Render

1. Décompressez l'archive et poussez le dossier du projet dans un dépôt GitHub.
2. Dans Render, sélectionnez **New + → Blueprint**, puis connectez le dépôt contenant `render.yaml`.
3. Render créera le service web et la base PostgreSQL décrite par le Blueprint. Le Blueprint utilise des offres payantes de démarrage pour éviter de dépendre d'une base gratuite éphémère ; vérifiez les tarifs Render avant de confirmer.
4. Le secret `JWT_SECRET` et le mot de passe de premier administrateur sont générés par Render. Après le premier déploiement, ouvrez **Environment** sur le service web pour lire `SEED_ADMIN_EMAIL` et `SEED_ADMIN_PASSWORD`. Conservez ces identifiants dans un gestionnaire de mots de passe, connectez-vous et remplacez immédiatement le mot de passe initial (la fonctionnalité de changement de mot de passe est à ajouter avant un usage public).
5. Attendez que `/api/health` renvoie `{"ok":true,"service":"NzadiTech Formation Manager","database":"connected"}`.

> Ne publiez jamais le fichier `.env`, les secrets ou des données réelles dans Git. Si vous créez la base manuellement, configurez `DATABASE_URL` sur le service web avec l'URL **interne** de la base Render et assurez-vous que le service et la base sont dans la même région.

## Lancer en local

Prérequis : Node.js 20+ et PostgreSQL accessible.

```bash
cp .env.example .env
# Modifiez DATABASE_URL, JWT_SECRET et SEED_ADMIN_PASSWORD dans .env
npm install
npm start
```

Puis ouvrez `http://localhost:3000`. L'application crée les tables et le premier centre au démarrage. Le premier compte super-administrateur est créé à partir des variables `SEED_ADMIN_*` uniquement si l'e-mail n'existe pas déjà.

## Routes principales

- `POST /api/auth/login`
- `GET /api/auth/me`
- `GET /api/dashboard`
- `GET|POST /api/students`, `/api/trainers`, `/api/courses`, `/api/sessions`, `/api/enrollments`, `/api/attendance`, `/api/payments`, `/api/messages`
- `PATCH /api/:resource/:id`
- `GET /api/reports/finance`
- `GET /api/health`

## Rôles initiaux

| Rôle | Accès principal |
|---|---|
| Super-administrateur / Directeur | Toutes les fonctions de gestion |
| Administrateur / secrétaire | Dossiers, inscriptions, sessions, présence, communications |
| Responsable pédagogique | Formations, sessions, inscriptions, présence, dossiers |
| Comptable | Dossiers apprenants, paiements, rapport financier |
| Chargé de communication | Dossiers, formateurs, communications |

## Sécurité et prochaines étapes obligatoires avant production

- Ajouter changement/réinitialisation de mot de passe et MFA pour rôles sensibles.
- Ajouter tests d'intégration/e2e et revue sécurité indépendante.
- Compléter toutes les contraintes de cohérence métier (y compris les références de paiement, remboursements et écritures atomiques).
- Chiffrer les secrets fournisseurs via un gestionnaire de secrets et vérifier les signatures de webhooks.
- Connecter un fournisseur SMS couvrant le Congo-Brazzaville et un fournisseur e-mail ; tester la délivrabilité, les coûts, les consentements et les opt-out.
- Définir sauvegarde et restauration vérifiée, politique de conservation et obligations locales avec un conseil compétent.

Le compte connecté peut changer son mot de passe depuis l'icône de clé en bas de la barre latérale. La modification invalide la session courante et demande une reconnexion.


## Déploiement Render gratuit

Le fichier `render.yaml` sélectionne le plan gratuit pour le service Web et PostgreSQL. Attention : le Web Service gratuit peut se mettre en veille, et la base PostgreSQL gratuite Render est temporaire (expiration au bout de 30 jours). Cette configuration est destinée à la démonstration et aux tests, pas à la conservation durable des données ni à la production. Consulte `docs/DEPLOIEMENT-RENDER.md` avant de déployer.
=======
# NZADI-Suivi-formation-
Gestionnaire de centre de formation 
>>>>>>> ba10971431b5b83e25eaf046f6179936ce256950
