# Working With Claude API

Proyecto de ejemplo en Python para experimentar con la API de Anthropic (Claude), combinando scripts y Jupyter Notebooks.

## Requisitos

- Python 3.14 (gestionado automáticamente por `uv`, ver `.python-version`)
- [`uv`](https://docs.astral.sh/uv/) como gestor de entorno y dependencias
- Windows + WSL2, con Visual Studio Code y la extensión **WSL** instalada en Windows
- Una API key de Anthropic

## Estructura

```
.
├── main.py                          # Punto de entrada de script
├── notebooks/
│   └── api_test_notebook.ipynb      # Notebook de prueba contra la API de Claude
├── .vscode/
│   ├── settings.json                # Intérprete, carga de .env, config de Jupyter
│   └── extensions.json              # Extensiones recomendadas
├── .env                              # Variables de entorno (no versionado)
├── pyproject.toml
└── uv.lock
```

## Configuración del entorno (Windows + WSL)

1. **Abrir el proyecto desde WSL en VS Code (Windows):**
   Desde una terminal WSL, situado en la carpeta del proyecto:
   ```bash
   code .
   ```
   Esto instala/actualiza automáticamente el *VS Code Server* dentro de WSL y abre una ventana de VS Code en modo remoto (`WSL: Ubuntu` o la distro correspondiente), mostrada en la esquina inferior izquierda.

2. **Extensiones recomendadas:**
   Al abrir el proyecto, VS Code sugerirá instalar las extensiones listadas en `.vscode/extensions.json`:
   - `ms-python.python` / `ms-python.vscode-pylance` — soporte de Python e IntelliSense
   - `ms-python.debugpy` — depuración
   - `ms-toolsai.jupyter` (+ `jupyter-renderers`) — soporte de Notebooks
   - `mikestead.dotenv` — resaltado de sintaxis para archivos `.env`

   Todas se instalan **dentro del entorno WSL** (no en Windows), que es donde se ejecuta el código.

3. **Instalar dependencias del proyecto:**
   ```bash
   uv sync
   ```
   Esto crea el entorno virtual `.venv` y instala tanto las dependencias de ejecución (`anthropic`, `python-dotenv`) como las de desarrollo (`ipykernel`, necesario para ejecutar notebooks).

4. **Variables de entorno:**
   Crear un archivo `.env` en la raíz del proyecto (ya ignorado por Git) con:
   ```
   ANTHROPIC_API_KEY=tu-api-key-aquí
   ```
   `.vscode/settings.json` configura `python.envFile` para que el intérprete y la terminal integrada de VS Code carguen automáticamente este archivo.

5. **Seleccionar el intérprete/kernel en VS Code:**
   VS Code detecta automáticamente `.venv` gracias a `python.defaultInterpreterPath`. Si se necesita seleccionar manualmente:
   - Script (`main.py`): `Ctrl+Shift+P` → *Python: Select Interpreter* → `.venv/bin/python`
   - Notebook: en la esquina superior derecha del notebook, *Select Kernel* → `.venv` (Python 3.14)

## Uso

**Ejecutar el script principal:**
```bash
uv run main.py
```

**Ejecutar el notebook de prueba:**
Abrir `notebooks/api_test_notebook.ipynb` en VS Code y ejecutar las celdas con el kernel de `.venv` seleccionado.

## Notas técnicas

- El proyecto usa `uv` como único gestor de dependencias; evitar `pip install` manual para mantener `pyproject.toml`/`uv.lock` como fuente de verdad.
- `ipykernel` se declara como dependencia de desarrollo (`--dev`) porque solo es necesaria para ejecutar notebooks, no en producción.
- El archivo `.env` nunca debe subirse al repositorio (ver `.gitignore`).
