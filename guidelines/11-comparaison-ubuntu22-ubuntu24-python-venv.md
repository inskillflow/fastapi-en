## Différences entre Ubuntu 22.04 et Ubuntu 24.04 pour Python et venv

| Élément | Ubuntu 22.04 | Ubuntu 24.04 |
|---|---|---|
| Version Python 3 par défaut | Python 3.10 | Python 3.12 |
| Commande recommandée | `python3` | `python3` |
| Vérifier la version | `python3 --version` | `python3 --version` |
| Installer l’environnement complet recommandé | `sudo apt install -y python3-full` | `sudo apt install -y python3-full` |
| Installer seulement le module venv de la version par défaut | `sudo apt install -y python3.10-venv` | `sudo apt install -y python3.12-venv` |
| Créer un environnement virtuel | `python3 -m venv myapp1` | `python3 -m venv myapp1` |
| Activer le venv | `source myapp1/bin/activate` | `source myapp1/bin/activate` |
| Ajouter la commande `python` | `sudo apt install -y python-is-python3` | `sudo apt install -y python-is-python3` |

---

> [!IMPORTANT]
> **Approche recommandée**
>
> ```bash
> sudo apt update
> sudo apt install -y python3-full git
> ```
>
> Cette approche est plus simple et plus complète.

> [!NOTE]
> **Approche ciblée par version**
>
> Pour Ubuntu 22.04 :
>
> ```bash
> sudo apt update
> sudo apt install -y python3.10-venv
> ```
>
> Pour Ubuntu 24.04 :
>
> ```bash
> sudo apt update
> sudo apt install -y python3.12-venv
> ```

> [!CAUTION]
> **If you also want the command `python`, install:**
>
> ```bash
> sudo apt install -y python-is-python3
> ```

---

## Commandes — Ubuntu 22.04

```bash
python3 --version
sudo apt update
sudo apt install -y python3-full git
# ou seulement :
sudo apt install -y python3.10-venv
python3 -m venv myapp1
source myapp1/bin/activate
python --version
pip list
```

---

## Commandes — Ubuntu 24.04

```bash
python3 --version
sudo apt update
sudo apt install -y python3-full git
# ou seulement :
sudo apt install -y python3.12-venv
python3 -m venv myapp1
source myapp1/bin/activate
python --version
pip list
```
