#uni 
Tool per gestire sia installazioni di python sia pacchetti.

Sostituisce pip e virtualenv.

Sostituisce parzialmente pipenv e poetry.

```bash
uv venv
uv pip install pacchetto

# per attivare il pacchetto
source .venv/bin/activate
# per disattivare
deactivate

# install from requirements file
uv pip install -r requirements.txt # oppure .lock

uv python install 3.12

uv venv --python 3.1
```
# project workflow con uv
1. crea cartella progetto
2. uv venv
3. source .venv/bin/activate
4. uv pip install
5. scrivi codice
6. genera lockfile: uv pip freeze > requirements.lock
7. deploy