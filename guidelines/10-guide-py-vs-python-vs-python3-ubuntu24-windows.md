# Comprendre `py`, `python`, `python3` et `venv` sous Windows et Ubuntu 24.04

## Objectif

Quand on travaille avec Python, on voit souvent plusieurs commandes qui se ressemblent :

- `py`
- `python`
- `python3`
- `python3.12`

Cela crée souvent de la confusion, surtout lorsqu’on passe de **Windows** à **Linux/Ubuntu**.

Ce document explique :

1. pourquoi la commande change selon le système ;
2. quand utiliser `py`, `python` ou `python3` ;
3. à quoi sert `venv` ;
4. pourquoi un environnement virtuel est important ;
5. quelles commandes utiliser dans notre projet **FastAPI + Streamlit**.

---

## 1) Pourquoi il existe plusieurs commandes Python

Python n’est pas lancé de la même façon sur tous les systèmes.

### Sous Windows

Sous Windows, on utilise souvent :

```bat
py
```

ou :

```bat
py -3.12
```

La commande `py` est le **Python Launcher for Windows**.  
Son rôle est de choisir la bonne version de Python installée sur la machine.

Exemple :

```bat
py -3.12 --version
```

Cela veut dire :

- lancer Python
- en demandant précisément la version **3.12**

Sur Windows, cette commande est très pratique lorsqu’il y a plusieurs versions de Python sur la même machine.

---

## 2) Pourquoi on n’utilise pas `py` sous Ubuntu

Sous **Ubuntu**, on n’utilise généralement **pas** `py`.

La commande standard est :

```bash
python3
```

Sur Ubuntu 24.04 :

- Python 3 est le Python recommandé ;
- la version Python 3 disponible par défaut pour Ubuntu 24.04 est **3.12** ;
- la commande normale à utiliser est donc `python3`. :contentReference[oaicite:1]{index=1}

Exemple :

```bash
python3 --version
```

Donc :

- **Windows** → souvent `py` ou `py -3.12`
- **Ubuntu** → généralement `python3`

---

## 3) Et la commande `python` alors ?

C’est là que beaucoup se trompent.

### Sous Ubuntu 24.04

La commande :

```bash
python
```

n’est **pas garantie** par défaut.

Ubuntu indique que, si on veut que `python` fonctionne comme alias de `python3`, on peut installer le paquet :

```bash
sudo apt install -y python-is-python3
```

Ce paquet crée un lien symbolique pour que :

```bash
python
```

pointe vers :

```bash
python3
``` 
:contentReference[oaicite:2]{index=2}

Donc :

- `python3` = commande fiable sous Ubuntu
- `python` = optionnel, si on installe `python-is-python3`

---

## 4) Résumé simple

### Règle pratique

#### Sous Windows
Utiliser généralement :

```bat
py -3.12
```

ou parfois :

```bat
python
```

#### Sous Ubuntu 24.04
Utiliser généralement :

```bash
python3
```

et éventuellement `python` seulement si on a installé :

```bash
sudo apt install -y python-is-python3
```

---

## 5) À quoi sert `venv` ?

`venv` signifie **virtual environment**  
en français : **environnement virtuel**.

Un environnement virtuel permet de créer un espace Python isolé pour un projet.

### Pourquoi c’est utile ?

Sans environnement virtuel :

- tous les paquets Python s’installent globalement ;
- les projets peuvent entrer en conflit ;
- une version installée pour un projet peut casser un autre projet.

Avec `venv` :

- chaque projet a ses propres dépendances ;
- le projet reste propre ;
- on évite les conflits entre bibliothèques.

Exemple :

```bash
python3 -m venv myapp1
```

Cette commande crée un dossier `myapp1` qui contient un environnement Python isolé.

---

## 6) Pourquoi `venv` ne marche pas toujours immédiatement sous Ubuntu ?

Sur Ubuntu, l’environnement Python minimal peut être installé sans tous les outils de développement.

C’est pour cela qu’Ubuntu recommande souvent d’installer :

```bash
sudo apt install -y python3-full
```

Ce paquet fournit un environnement Python plus complet, incluant les composants utiles pour le développement, notamment `venv`. :contentReference[oaicite:3]{index=3}

Donc, si cette commande échoue :

```bash
python3 -m venv myapp1
```

il faut souvent installer ou réinstaller :

```bash
sudo apt install -y python3-full
```

---

## 7) Pourquoi on active l’environnement virtuel ?

Créer le venv ne suffit pas.

Après la création, il faut **l’activer**.

### Sous Ubuntu / Linux

```bash
source myapp1/bin/activate
```

### Sous Windows CMD

```bat
.\myapp1\Scripts\activate
```

### Sous Windows PowerShell

```powershell
.\myapp1\Scripts\Activate.ps1
```

Quand l’environnement est activé :

- `python` pointe vers le Python du projet ;
- `pip` installe les paquets dans ce projet uniquement ;
- on évite de polluer le système.

---

## 8) Différence entre `pip` et `pip3`

Historiquement, sur Linux, on distinguait souvent :

- `pip` pour Python 2
- `pip3` pour Python 3

C’est une ancienne habitude qu’on rencontre encore. Une fois l’environnement virtuel activé, `pip` pointe normalement vers le pip du venv. :contentReference[oaicite:4]{index=4}

Dans notre projet, après activation du venv, on peut donc utiliser :

```bash
pip install -r requirements.txt
```

---

## 9) Cas concret : notre projet FastAPI + Streamlit sous Ubuntu 24.04

Voici la logique complète.

### Étape 1 — Installer Python et Git

```bash
sudo apt update
sudo apt install -y python3-full git
```

### Étape 2 — Vérifier Python 3

```bash
python3 --version
```

### Étape 3 — Créer le dossier du projet

```bash
cd ~/Downloads
mkdir application1
cd application1
```

### Étape 4 — Cloner le dépôt

```bash
git clone https://github.com/inskillflow/demo_api_1_simple_fastapi_app.git .
```

### Étape 5 — Ouvrir le projet

```bash
code .
```

### Étape 6 — Créer l’environnement virtuel

```bash
python3 -m venv myapp1
```

### Étape 7 — Activer l’environnement virtuel

```bash
source myapp1/bin/activate
```

### Étape 8 — Installer les dépendances

```bash
pip install -r requirements.txt
```

### Étape 9 — Voir les paquets installés

```bash
pip list
```

---

## 10) Pourquoi on ouvre deux terminaux ?

Dans ce projet, il y a deux parties :

- le **backend** avec FastAPI
- le **frontend** avec Streamlit

Il est donc pratique d’avoir :

- **Terminal 1** = backend
- **Terminal 2** = frontend

Les deux doivent avoir le même environnement virtuel activé.

---

## 11) Terminal 1 = backend

### Commandes

```bash
cd ~/Downloads/application1
python3 -m venv myapp1
source myapp1/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload
```

### Explication

- `uvicorn` lance le serveur FastAPI
- `main:app` signifie :
  - fichier `main.py`
  - variable `app`
- `--reload` redémarre automatiquement le serveur si le code change

### Très important

Ne pas lancer :

```bash
python main.py
```

dans ce projet, car l’application FastAPI est prévue pour être exécutée avec :

```bash
uvicorn main:app --reload
```

---

## 12) Terminal 2 = frontend

### Commandes

```bash
cd ~/Downloads/application1
source myapp1/bin/activate
streamlit run frontend.py
```

### Ou

```bash
python -m streamlit run frontend.py
```

### Explication

Cela lance l’interface graphique Streamlit qui communique avec l’API.

---

## 13) Si `python3` ne fonctionne pas

Essayer :

```bash
python --version
```

Si `python` n’existe pas non plus, installer l’alias :

```bash
sudo apt install -y python-is-python3
```

puis vérifier :

```bash
python --version
``` 
:contentReference[oaicite:5]{index=5}

---

## 14) Si `python3 -m venv myapp1` échoue

Réinstaller l’environnement Python complet :

```bash
sudo apt update
sudo apt install -y python3-full
```

puis recommencer :

```bash
python3 -m venv myapp1
``` 
:contentReference[oaicite:6]{index=6}

---

## 15) Si on veut donner les droits sudo à un utilisateur

Exemple :

```bash
sudo usermod -aG sudo eleve
su - eleve
groups
sudo whoami
```

### Explication

- `usermod -aG sudo eleve` : ajoute `eleve` au groupe `sudo`
- `su - eleve` : ouvre une session avec l’utilisateur `eleve`
- `groups` : affiche les groupes de l’utilisateur
- `sudo whoami` : vérifie que l’utilisateur peut utiliser `sudo`

### Attention

Cette opération donne des privilèges administrateur.  
Elle ne doit être faite que si c’est réellement nécessaire.

---

## 16) Version finale des commandes Ubuntu 24.04

> [!TIP]
> **Installation de Python et initialisation du projet**
>
> ```bash
> sudo apt update
> sudo apt install -y python3-full git
> cd ~/Downloads
> mkdir application1
> cd application1
> git clone https://github.com/inskillflow/demo_api_1_simple_fastapi_app.git .
> code .
> ```

> [!CAUTION]
> **On Ubuntu 24.04, `python3` is the default system Python.**
>
> ```bash
> python3 --version
> ```

> [!CAUTION]
> **If you want the command `python`, install:**
>
> ```bash
> sudo apt install -y python-is-python3
> python --version
> ```

---

## OPEN A NEW TERMINAL (TERMINAL 1)

```bash
cd ~/Downloads/application1
python3 --version
python3 -m venv myapp1
source myapp1/bin/activate
python --version
pip install -r requirements.txt
pip list
```

> [!WARNING]
> **Run the following commands only if you really want to give the user `eleve` sudo privileges:**
>
> ```bash
> sudo usermod -aG sudo eleve
> su - eleve
> groups
> sudo whoami
> ```

> [!CAUTION]
> **If `python3 -m venv myapp1` does not work, reinstall the full Python package:**
>
> ```bash
> sudo apt update
> sudo apt install -y python3-full
> ```

> [!CAUTION]
> **If `python3` does not work on your machine, try with `python`:**
>
> ```bash
> python --version
> python -m venv myapp1
> ```

---

## OPEN A NEW TERMINAL (TERMINAL 2)

```bash
cd ~/Downloads/application1
source myapp1/bin/activate
```

---

> [!IMPORTANT]
> **From now on:**
>
> - **Terminal 1** = backend terminal
> - **Terminal 2** = frontend terminal

---

## GO TO TERMINAL 1 (BACKEND TERMINAL)

```bash
uvicorn main:app --reload
```

> [!WARNING]
> **Do not run:**
>
> ```bash
> python main.py
> ```

---

## GO TO TERMINAL 2 (FRONTEND TERMINAL)

```bash
streamlit run frontend.py
```

### OR

```bash
python -m streamlit run frontend.py
```

---

> [!NOTE]
> **Next steps**
>
> - Analyse `backend.py`
> - Analyse `frontend.py`
> - Do Evaluation 1: creating the API
> - Do Evaluation 2: creating the UI for your API

---

## Conclusion

Il faut retenir la règle suivante :

- **Windows** → souvent `py`
- **Ubuntu** → généralement `python3`
- `python` sous Ubuntu est optionnel
- `venv` sert à isoler le projet
- on active le venv avant d’installer les dépendances ou de lancer l’application

Autrement dit :

- **ne pas recopier aveuglément les commandes Windows sous Ubuntu**
- **adapter la commande Python au système utilisé**
