# Environnement de TP : n8n & Local AI (Self-Hosted)

Bienvenue dans cet environnement de travaux pratiques (TP) conçu pour vous faire découvrir l'automatisation de workflows combinée à de l'Intelligence Artificielle exécutée localement.

Ce dépôt utilise le **n8n Self-hosted AI Starter Kit** préconfiguré et adapté pour fonctionner directement et sans effort au sein de **GitHub Codespaces**.

---

## 🚀 Prérequis et Démarrage rapide

### 1. Prérequis : Compte GitHub
Avant de commencer, vous devez disposer d'un compte GitHub. Si ce n'est pas le cas :
- Rendez-vous sur [github.com](https://github.com/).
- Cliquez sur **Sign up** et suivez les instructions pour créer votre compte gratuitement.

### 2. Démarrage sur GitHub Codespaces
Une fois votre compte GitHub actif et connecté :

1. Ouvrez ce dépôt GitHub.
2. Cliquez sur le bouton **Code** en haut à droite.
3. Allez dans l'onglet **Codespaces** et cliquez sur **Create codespace on main**.
3. L'environnement va se construire automatiquement. Cette étape démarre plusieurs conteneurs Docker en arrière-plan :
   - **n8n** : L'outil de création de workflows.
   - **PostgreSQL** : La base de données pour sauvegarder vos workflows.
   - **Ollama** : Le moteur d'exécution local de modèles de langage (LLM).
   - **Qdrant** : La base de données vectorielle pour donner de la mémoire à votre IA.
4. Une fois l'initialisation terminée, VS Code Web s'ouvre.

---

## 🔌 Accéder aux outils

Pour accéder aux interfaces des différents outils, rendez-vous dans l'onglet **Ports** de la console VS Code (en bas) et cliquez sur le lien généré dans la colonne **Local Address** du service correspondant :

* **n8n (Interface Web)** : port `5678`
* **Ollama (API)** : port `11434`
* **Qdrant (API/Dashboard)** : port `6333`

> [!IMPORTANT]
> Lors du premier démarrage, le conteneur `ollama-pull-llama` télécharge automatiquement le modèle d'IA léger **Llama 3.2** (environ 2 Go). Cela peut prendre 1 à 3 minutes selon la vitesse de connexion du Codespace. Vous pouvez suivre l'avancement en consultant les logs Docker du conteneur `ollama-pull-llama`.

---

## 🎓 Éléments inclus dans le TP

### 1. Workflow de démonstration
À l'ouverture de n8n (via le port `5678` dans l'onglet **Ports**), un workflow de démonstration est automatiquement importé et prêt à l'emploi.
Il s'agit d'une chaîne LLM simple :
`Chat Trigger (Déclencheur de Chat) ➔ Basic LLM Chain ➔ Ollama Chat Model`

### 2. Identifiants préconfigurés
Les connexions réseau vers **Ollama** et **Qdrant** sont déjà créées et associées aux nœuds correspondants sous les noms :
* `Local Ollama service`
* `Local QdrantApi database`

### 3. Dossier partagé
Le dossier local `./shared` est monté dans le conteneur n8n sur le chemin `/data/shared`. Vous pouvez l'utiliser avec les nœuds de lecture/écriture de fichiers de n8n pour manipuler des documents locaux dans vos workflows.

---

## 🛠️ Tester votre premier workflow d'IA

1. Ouvrez l'interface n8n (via le port `5678` dans l'onglet **Ports**).
2. Ouvrez le workflow importé nommé **Demo workflow**.
3. Cliquez sur le bouton **Chat** tout en bas de la page du workflow.
4. Saisissez un message (ex: *"Bonjour, qui es-tu ?"*) et validez. Le modèle local `llama3.2` hébergé sur Ollama va générer sa réponse directement dans l'interface !
