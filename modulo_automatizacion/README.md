# Prueba-automatizacion-sauceDemo
 
## Descripción
Smoke Test de login para https://www.saucedemo.com/ usando Selenium + Behave con patrón POM (Page Object Model).

## Requisitos
- Python 3.9+
- Google Chrome instalado

## Instalación
```bash
python -m venv .venv
source .venv/bin/activate   # En macOS/Linux
# En Windows
.venv\\Scripts\\activate
pip install -r requirements.txt
```

## Ejecución
```bash
behave -f pretty
```
Gracias a `behave.ini` puedes ejecutar el comando desde la raíz del proyecto.

Notas:
- El driver de Chrome se gestiona automáticamente con `webdriver-manager`.
- Para ejecutar en headless, descomenta la línea exacta en `modulo_automatizacion/features/environment.py`:
  ```python
  options.add_argument("--headless=new")
  ```

## Estructura
 - modulo_automatizacion/
   - pages/
     - login_page.py
     - inventory_page.py
   - features/
     - login.feature
     - steps/
       - login_steps.py
     - environment.py
   - __init__.py
   - README.md
   - requirements.txt
 - behave.ini
 - requirements.txt (raíz del proyecto)

## Escenarios cubiertos
- Login exitoso con credenciales válidas.
- Login fallido con contraseña incorrecta.
- Validación de campos obligatorios (usuario/contraseña vacíos).

## Solución de problemas
- Si aparece "No steps directory" o no encuentra `features`, verifica que `behave.ini` tenga:
  ```ini
  paths = modulo_automatizacion/features
  ```
- Si Chrome no abre o el driver falla, actualiza Chrome y reinstala dependencias:
  ```bash
  pip install -r requirements.txt
  ```