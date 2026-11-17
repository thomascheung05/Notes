# Python venv

## Create

```bash
python3 -m venv venv
```

## Activate

| Shell / OS | Command |
|---|---|
| Linux / Mac (bash, zsh) | `source venv/bin/activate` |
| fish | `source venv/bin/activate.fish` |
| Windows | `venv\Scripts\activate` |

Leave the venv with `deactivate`.

## Requirements

```bash
pip install -r requirements.txt  # install from a requirements file
pip freeze > requirements.txt    # save current dependencies
```
