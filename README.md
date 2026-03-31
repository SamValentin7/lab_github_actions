# LUCRARE DE LABORATOR 2: INTRODUCERE ÎN GITHUB ACTIONS

## Obiective

• Înțelegerea conceptului de CI/CD (Continuous Integration / Continuous Deployment).
• Crearea primului workflow GitHub Actions.
• Automatizarea verificării codului la push și pull request.

---

## Realizați următoarele sarcini:

### 1. Pregătirea Repozitoriului

- Creează un nou repozitoriu GitHub numit `lab_github_actions`.
- Clonează repozitoriul local:
  ```bash
  git clone https://github.com/<username>/lab_github_actions.git
  ```
- Intră în directorul proiectului:
  ```bash
  cd lab_github_actions
  ```

### 2. Crearea unui fișier simplu

- Creează un fișier `script.py` cu următorul conținut:
  ```python
  print("Hello, GitHub Actions!")
  ```
- Adaugă, comite și urcă modificările:
  ```bash
  git add script.py
  git commit -m "Adaugă script Python simplu"
  git push origin main
  ```

### 3. Crearea Workflow-ului GitHub Actions

- În repozitoriu, creează următoarea structură de directoare:
  ```
  .github/workflows/
  ```
- Creează un fișier YAML nou: `.github/workflows/python-app.yml`

**Conținutul minim:**
```yaml
name: Python application

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4

    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: '3.x'

    - name: Run script
      run: python script.py
```

### 4. Testare Workflow

- Fă o mică modificare în `script.py` (de exemplu, schimbă mesajul).
- Comite și împinge modificările:
  ```bash
  git add script.py
  git commit -m "Update mesaj script"
  git push
  ```
- Mergi pe pagina **GitHub → Actions** și vezi rularea automată a workflow-ului.

### 5. Extensie opțională (pentru avansați)

- Adaugă un fișier de test - `test_script.py`:
  ```python
  def test_example():
      assert 1 + 1 == 2
  ```

- Modifică workflow-ul să ruleze și pytest:

  ```yaml
  - name: Install pytest
    run: pip install pytest

  - name: Run tests
    run: pytest
