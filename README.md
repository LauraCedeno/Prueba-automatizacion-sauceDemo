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
pip install -r 
```

## Ejecución
```bash
behave -f pretty
```

Notas:
- El driver de Chrome se gestiona automáticamente con `webdriver-manager`.
- Para ejecutar en headless, descomenta la línea `--headless=new` en `features/environment.py`.

## Estructura
- pages/
  - login_page.py
  - inventory_page.py
- features/
  - login.feature
  - steps/
    - login_steps.py
  - environment.py
- behave.ini
- requirements.txt

## Escenarios cubiertos
- Login exitoso con credenciales válidas.
- Login fallido con contraseña incorrecta.
- Validación de campos obligatorios (usuario/contraseña vacíos).