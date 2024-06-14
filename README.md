# Python-Security-Tests
name: Python Security Tests

on:
  push:
    branches: [ main ]

jobs:
  security-tests:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt  # se houver um arquivo de requisitos

      - name: Run Bandit security tests
        run: |
          pip install bandit
          bandit -r . -ll  # Executa o Bandit recursivamente no diretório atual
