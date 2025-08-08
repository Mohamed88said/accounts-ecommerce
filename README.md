# Accounts Ecommerce

Projet Django & Django REST Framework de gestion des comptes utilisateurs pour une plateforme e-commerce moderne.

## Table des matières

- [Aperçu du projet](#aperçu-du-projet)
- [Fonctionnalités](#fonctionnalités)
- [Arborescence du projet](#arborescence-du-projet)
- [Templates à créer](#templates-à-créer)
- [Installation](#installation)
- [Configuration](#configuration)
- [API REST](#api-rest)
- [Gestion des permissions et rôles](#gestion-des-permissions-et-rôles)
- [Tests](#tests)
- [Roadmap / TODO](#roadmap--todo)
- [Contribuer](#contribuer)
- [Licence](#licence)

---

## Aperçu du projet

Ce projet propose une gestion complète des utilisateurs orientée e-commerce : authentification, profils, rôles, gestion avancée du compte, sécurité, API RESTful, templates personnalisés, gestion des emails, etc.

---

## Fonctionnalités

### Authentification et gestion de compte

- Inscription avec email/username
- Connexion / déconnexion
- Authentification par email (activation obligatoire)
- Réinitialisation de mot de passe (email)
- Changement de mot de passe
- Modification de l’e-mail (avec confirmation)
- Suppression de compte (soft/hard delete)
- Gestion des sessions actives

### Profils utilisateurs

- Création automatique de profil à l’inscription
- Modification du profil (nom, prénom, avatar, téléphone, adresse, etc.)
- Upload/modification d’avatar
- Gestion de préférences (newsletters, notifications)
- Historique de connexion
- Vue publique/privée du profil

### Gestion des rôles et permissions

- Rôles standards : utilisateur, vendeur, staff, admin, superadmin
- Permissions associées à chaque rôle
- Interface de gestion des utilisateurs et des rôles (admin et API)
- Changement de rôle par admin
- Historique des changements de rôle

### Sécurité

- Validation des emails (token/expiration)
- Limitation des tentatives de connexion
- Authentification à deux facteurs (2FA, optionnel)
- Gestion des sessions et tokens (JWT, refresh)
- RGPD : exportation et suppression des données

### API REST (Django REST Framework)

- Endpoints pour toutes les fonctionnalités ci-dessus
- Authentification JWT + sessions classiques
- Permissions fines par endpoint/role
- Pagination, filtrage, recherche
- Documentation Swagger/OpenAPI

### Administration & gestion

- Interface d’administration Django customisée
- Gestion avancée des utilisateurs, profils, rôles, logs
- Export CSV/Excel des utilisateurs
- Dashboard statistiques utilisateurs

### Emailing & notifications

- Templates d’email personnalisés (inscription, reset, etc.)
- Notifications par email et internes (préférences utilisateur)
- Journalisation des emails envoyés

---

## Arborescence du projet

```
accounts-ecommerce/
├── manage.py
├── accounts_ecommerce/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── accounts/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── tests.py
│   ├── urls.py
│   ├── views.py
│   ├── migrations/
│   │   └── __init__.py
│   └── templates/
│       └── accounts/
│           ├── base.html
│           ├── login.html
│           ├── register.html
│           ├── profile.html
│           ├── profile_edit.html
│           ├── password_reset.html
│           ├── password_reset_confirm.html
│           ├── email_confirmation.html
│           ├── email_change.html
│           ├── account_deleted.html
│           ├── dashboard.html
│           ├── admin_user_list.html
│           ├── admin_user_edit.html
│           └── emails/
│               ├── activation_email.html
│               ├── password_reset_email.html
│               ├── email_change_email.html
│               └── notification_email.html
```

---

## Templates à créer

### Pages utilisateurs

- `base.html` – Template de base du site
- `login.html` – Connexion
- `register.html` – Inscription
- `profile.html` – Vue du profil utilisateur
- `profile_edit.html` – Modification du profil
- `password_reset.html` – Demande de réinitialisation de mot de passe
- `password_reset_confirm.html` – Confirmation de réinitialisation
- `email_confirmation.html` – Confirmation de l’email
- `email_change.html` – Changement d’adresse email
- `account_deleted.html` – Confirmation de suppression du compte
- `dashboard.html` – Tableau de bord utilisateur

### Administration

- `admin_user_list.html` – Liste des utilisateurs/admin
- `admin_user_edit.html` – Modification d’un utilisateur/admin

### Emails (dans `templates/accounts/emails/`)

- `activation_email.html` – Email d’activation de compte
- `password_reset_email.html` – Email de reset de mot de passe
- `email_change_email.html` – Email de confirmation de changement d’email
- `notification_email.html` – Notification générique

---

## Installation

```bash
git clone https://github.com/Mohamed88said/accounts-ecommerce.git
cd accounts-ecommerce
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp accounts_ecommerce/.env.example accounts_ecommerce/.env
# Editer les variables d’environnement selon besoin
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

---

## Configuration

- Variables d’environnement dans `.env`
- Configuration email SMTP (pour l’envoi des emails)
- Configuration du stockage des fichiers médias (avatars, etc.)
- Secret Key, JWT Secret, etc.

---

## API REST

- `/api/auth/register/` – Inscription
- `/api/auth/login/` – Connexion
- `/api/auth/logout/`
- `/api/auth/password-reset/`
- `/api/auth/email-confirm/`
- `/api/profile/` – Récupération/modification profil
- `/api/admin/users/` – Liste/admin utilisateurs (staff)
- `/api/roles/` – Gestion des rôles
- ... (voir documentation Swagger intégrée au projet)

---

## Gestion des permissions et rôles

- User : accès à son profil, modification, commandes, etc.
- Vendeur : accès à la gestion de ses produits/profils
- Staff : accès à la modération, gestion utilisateurs
- Admin : gestion complète
- Superadmin : gestion technique et des permissions

---

## Tests

- Couverture des modèles, vues, API, permissions, templates
- Tests unitaires et d’intégration
- Commande : `python manage.py test`

---

## Roadmap / TODO

- [ ] Ajouter la gestion de l’authentification sociale (Google, Facebook)
- [ ] Intégrer la 2FA (OTP/email)
- [ ] Système de notifications internes en temps réel
- [ ] Export et suppression de compte (RGPD)
- [ ] Optimisation des performances (caching, pagination avancée)
- [ ] Amélioration UX/UI (responsive, design moderne)
- [ ] Documentation complète (Swagger, doc utilisateur)
- [ ] Déploiement (Docker, CI/CD)

---

## Contribuer

Les contributions sont les bienvenues !  
Voir [CONTRIBUTING.md](CONTRIBUTING.md) pour plus d’informations.

---

## Licence

Ce projet est sous licence MIT.