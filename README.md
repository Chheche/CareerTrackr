# CareerTrackr

**CareerTrackr** est une application web intelligente permettant de **centraliser et suivre automatiquement vos candidatures** à partir de vos e-mails Gmail.  
Elle combine une interface web moderne type **Trello** et une analyse automatisée des e-mails via **Python + NLP (spaCy)**.

---

## 💡 Description

CareerTrackr vous aide à **gérer vos candidatures** de manière automatisée.  
Dès la connexion avec votre compte Gmail (via OAuth 2.0), un script Python analyse vos e-mails de candidatures pour en extraire les informations clés :  
- **Poste**  
- **Entreprise**  
- **Date de réception**  
- **Statut** (envoyée, entretien, refusée, en attente)

Ces informations sont ensuite **stockées dans une base PostgreSQL** et affichées dans une interface web intuitive comportant trois colonnes :  
- 📥 **Accusés de réception**  
- 🗓️ **Entretiens prévus**  
- ❌ **Candidatures refusées**

Une section dédiée vous permet également de **téléverser et visualiser votre CV** directement dans l’application.

---

## ⚙️ Fonctionnalités

- 🔐 **Connexion sécurisée via Google OAuth 2.0**
- 📧 **Récupération automatique des e-mails Gmail**
- 🧠 **Analyse du contenu avec spaCy (NLP en français)**
- 🏷️ **Extraction des informations clés : poste, entreprise, date, statut**
- 💾 **Insertion automatique dans une base PostgreSQL**
- 🗂️ **Interface web type Trello (Spring Boot + JS + HTML/CSS)**
- 📄 **Visionneuse intégrée pour le CV**

---

## Technologies utilisées

- **Back-end** : Spring Boot (Java)
- **Front-end** : HTML / CSS / JavaScript
- **Analyse mails** : Python 3, spaCy
- **Base de données** : PostgreSQL
- **Authentification** : Google OAuth 2.0
- **API** : Google Gmail API

---

## 🧩 Notes techniques

* Le script Python communique avec Spring Boot via **stdout en JSON**.
* Un modèle **spaCy NER** est utilisé pour reconnaître les métiers dans les e-mails.
* La table des candidatures se met à jour automatiquement à chaque nouvelle connexion.

---

## Prérequis

### Logiciels
- Python **3.8+**
- Java **17+**
- PostgreSQL
- Google Cloud Account (pour l’API Gmail)

---

## 🪜 Installation

Ouvrir le dossier du projet dans votre IDE.

### Configuration du projet Spring Boot

1. **Aucune création manuelle de projet n’est nécessaire** :
   Le projet Spring Boot est déjà prêt à être importé.
   → Il suffit de l’ouvrir directement dans VS Code ou IntelliJ (comme projet Maven/Gradle).

2. Assurez-vous d’avoir **Java 17+** et **Maven** installés.

3. Modifier le fichier `application.properties` si besoin :

   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/careertrackr
   spring.datasource.username=postgres
   spring.datasource.password=*****
   ```


### Base de données PostgreSQL

Créer une base nommée :

```sql
CREATE DATABASE careertrackr;
```


### Script Python (analyse des mails)

#### Installer les dépendances Python :

```bash
pip install google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client spacy psycopg2-binary
python -m spacy download fr_core_news_md
```


#### Fichier `credentials.json`

🔑 Mise en place de l’OAuth 2.0 Google

Étape 1 : Créer un projet sur Google Cloud

- Rendez-vous sur Google Cloud Console.
- Connectez-vous avec votre compte Gmail.
- Cliquez sur “Sélectionner un projet” → “Nouveau projet”.
- Donnez un nom (ex. CareerTrackr) puis cliquez sur Créer.


Étape 2 : Activer l’API Gmail

- Dans le menu API et services → Bibliothèque, cherchez Gmail API.
- Cliquez sur Activer.


Étape 3 : Créer les identifiants OAuth2

- Allez dans API et services → Identifiants.
- Cliquez sur Créer des identifiants → ID client OAuth.
- Configurez l’écran de consentement :
- Type : Externe
- Nom d’application : CareerTrackr
- Email de contact : votre adresse Gmail
- Sélectionnez Application de bureau (pour les tests locaux).

Notez bien le Client ID et le Client Secret.

Créez ensuite un fichier credentials.json dans le dossier python du projet et ajoutez ceci :

```json
{
  "installed": {
    "client_id": "VOTRE_CLIENT_ID",
    "project_id": "VOTRE_NOM_DE_PROJET",
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://oauth2.googleapis.com/token",
    "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
    "client_secret": "VOTRE_CLIENT_SECRET",
    "redirect_uris": ["http://localhost/"]
  }
}
```

Le fichier **token.json** est généré ensuite automatiquement lors de la première exécution.


## 🪜 Lancement du projet
1. Lancer le projet avec :

   ```bash
   mvn spring-boot:run
   ou
   .\mvnw clean spring-boot:run
   ```

2. Accéder à l’interface web sur :
   `http://localhost:8080`


Rafael BARRETO PANNETIER — Étudiant ingénieur en informatique
