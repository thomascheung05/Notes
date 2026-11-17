# PyInstaller

## Quick build (once the .spec file exists)

1. Make sure you're in the venv with all packages installed
2. Make sure `pyinstaller` is installed too
3. Run:

```bash
pyinstaller firecan_main.spec
```

This builds the app into `dist/`.

## 1. Setup

Build from a clean venv:

```bash
python -m venv pyinstaller_test_env
source pyinstaller_test_env/bin/activate   # fish: source pyinstaller_test_env/bin/activate.fish
pip install -r requirements.txt
pip install pyinstaller
```

## 2. Make Flask bundle-aware

`--onefile` extracts to a temp dir (`sys._MEIPASS`) at runtime. Point the static folder there or assets will 404:

```python
import sys, os
from flask import Flask

if getattr(sys, 'frozen', False):
    app = Flask(__name__, static_folder=os.path.join(sys._MEIPASS, 'static'))
else:
    app = Flask(__name__)
```

## 3. Use a persistent data directory

Don't base `work_dir` on `os.getcwd()` or `__file__`. Both break or reset in a frozen exe. Use an OS-standard app-data folder instead:

```python
from pathlib import Path

def get_work_dir() -> Path:
    if getattr(sys, 'frozen', False):
        if sys.platform == 'darwin':
            base = Path.home() / "Library/Application Support/FIRECAN"
        elif sys.platform == 'win32':
            base = Path(os.environ['APPDATA']) / "FIRECAN"
        else:
            base = Path.home() / ".firecan"
    else:
        base = Path(__file__).parent
    base.mkdir(parents=True, exist_ok=True)
    return base
```

## 4. Generate & build

```bash
pyi-makespec --onefile --add-data "static:static" firecan_main.py
pyinstaller firecan_main.spec
```

Keep `datas` minimal (`[('static', 'static')]`). PyInstaller's built-in hooks already handle geopandas/pyproj/shapely. Only add `collect_data_files()` / `collect_submodules()` for a package if you hit a runtime error without it.

## 5. Test in isolation

```bash
deactivate
cd dist
./firecan_main
```

Move the exe to a fresh folder (e.g. Desktop) and re-run to confirm data storage works outside the repo.

Watch for:

| Problem | Fix |
|---|---|
| `ModuleNotFoundError` | Add the module to `hiddenimports` |
| GDAL/PROJ errors | Add `collect_data_files('pyproj')` |
| Static files 404 | Check step 2 |
| macOS Gatekeeper warning | Expected: right-click → Open |

## 6. Git vs. Releases

- **Commit:** source code + `firecan_main.spec`
- **.gitignore:** `build/`, `dist/`
- **Release asset:** zip of `dist/` contents only (never `build/`)

```bash
cd dist && zip -r FIRECAN-macos.zip firecan_main
```

## 7. Rebuilding

```bash
git pull
pip install -r requirements.txt   # if deps changed
pyinstaller firecan_main.spec
```

Update the spec when you:

- add a package
- add new data files
- hit a `ModuleNotFoundError`
- change the entry point or icon

No spec changes are needed for ordinary code edits.
